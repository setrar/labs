## :a: Adapting the stock portfolio example

:bulb: in the `openwire` folder

:round_pushpin: Add the `Consumer` Java Source Code

- [ ] use the `Consumer` Class as an example

```java
package org.apache.activemq.book.ch4.openwire;

import javax.jms.Connection;
import javax.jms.ConnectionFactory;
import javax.jms.Destination;
import javax.jms.JMSException;
import javax.jms.MessageConsumer;
import javax.jms.Session;

import org.apache.activemq.ActiveMQConnectionFactory;

public class Consumer {

    private static transient ConnectionFactory factory;
    private transient Connection connection;
    private transient Session session;
    
    public Consumer(String brokerURL) throws JMSException {
    	factory = new ActiveMQConnectionFactory(brokerURL);
    	connection = factory.createConnection();
        connection.start();
        session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
    }
    
    public void close() throws JMSException {
        if (connection != null) {
            connection.close();
        }
    }    
    
    public static void main(String[] args) throws JMSException {
    	if (args.length == 0) {
    		System.err.println("Please define connection URI!");
    		return;
    	}
    	
    	//define connection URI
    	Consumer consumer = new Consumer(args[0]);
    	
    	//extract topics from the rest of arguments
    	String[] topics = new String[args.length - 1];
    	System.arraycopy(args, 1, topics, 0, args.length - 1);
    	for (String stock : topics) {
    		Destination destination = consumer.getSession().createTopic("STOCKS." + stock);
    		MessageConsumer messageConsumer = consumer.getSession().createConsumer(destination);
    		messageConsumer.setMessageListener(new Listener());
    	}
    }
	
	public Session getSession() {
		return session;
	}

}
```

- [ ] you need the `Listener` Class to retrieve your message (same source code as `ch3`)

```java
package org.apache.activemq.book.ch4.openwire;

import java.text.DecimalFormat;

import javax.jms.MapMessage;
import javax.jms.Message;
import javax.jms.MessageListener;

public class Listener implements MessageListener {

	public void onMessage(Message message) {
		try {
			MapMessage map = (MapMessage)message;
			String stock = map.getString("stock");
			double price = map.getDouble("price");
			double offer = map.getDouble("offer");
			boolean up = map.getBoolean("up");
			DecimalFormat df = new DecimalFormat( "#,###,###,##0.00" );
			System.out.println(stock + "\t" + df.format(price) + "\t" + df.format(offer) + "\t" + (up?"up":"down"));
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}
```

- [ ] Let's package the project

```
mvn package
```

- [ ] :rocket: Let's run the app using `Maven` executable plugin `exec:<language>` by `defining` the `exec.mainClass` system property (or argument) and `defining` the `exec.args` property to pass the stock tickers.

* using `tcp` protocol

```
mvn exec:java --define exec.mainClass=org.apache.activemq.book.ch4.openwire.Consumer --define exec.args="tcp://localhost:61616 CSCO ORCL"
```

* using `nio` protocol

```
mvn exec:java --define exec.mainClass=org.apache.activemq.book.ch4.openwire.Consumer --define exec.args="nio://localhost:61616 CSCO ORCL"
```


:round_pushpin: Add the `Publisher` Java Source Code

- [ ] use the `Publisher` Class as an example

```java
package org.apache.activemq.book.ch4.openwire;

import java.util.Hashtable;
import java.util.Map;

import javax.jms.Connection;
import javax.jms.ConnectionFactory;
import javax.jms.Destination;
import javax.jms.JMSException;
import javax.jms.MapMessage;
import javax.jms.Message;
import javax.jms.MessageProducer;
import javax.jms.Session;

import org.apache.activemq.ActiveMQConnectionFactory;
import org.apache.activemq.command.ActiveMQMapMessage;

public class Publisher {
	
    private int MAX_DELTA_PERCENT = 1;
    private Map<String, Double> LAST_PRICES = new Hashtable<String, Double>();
    private static int count = 10;
    private static int total;
    
    private static transient ConnectionFactory factory;
    private transient Connection connection;
    private transient Session session;
    private transient MessageProducer producer;
    
    public Publisher(String brokerURL) throws JMSException {
    	factory = new ActiveMQConnectionFactory(brokerURL);
    	connection = factory.createConnection();
        connection.start();
        session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        producer = session.createProducer(null);
    }
    
    public void close() throws JMSException {
        if (connection != null) {
            connection.close();
        }
    }
    
    public static void main(String[] args) throws JMSException {
    	if (args.length == 0) {
    		System.err.println("Please define connection URI!");
    		return;
    	}

    	//define connection URI
    	Publisher publisher = new Publisher(args[0]);


    	//extract topics from the rest of arguments
    	String[] topics = new String[args.length - 1];
    	System.arraycopy(args, 1, topics, 0, args.length - 1);
        while (total < 1000) {
            for (int i = 0; i < count; i++) {
                publisher.sendMessage(topics);
            }
            total += count;
            System.out.println("Published '" + count + "' of '" + total + "' price messages");
            try {
              Thread.sleep(1000);
            } catch (InterruptedException x) {
            }
          }
        publisher.close();
    }

    protected void sendMessage(String[] stocks) throws JMSException {
        int idx = 0;
        while (true) {
            idx = (int)Math.round(stocks.length * Math.random());
            if (idx < stocks.length) {
                break;
            }
        }
        String stock = stocks[idx];
        Destination destination = session.createTopic("STOCKS." + stock);
        Message message = createStockMessage(stock, session);
        System.out.println("Sending: " + ((ActiveMQMapMessage)message).getContentMap() + " on destination: " + destination);
        producer.send(destination, message);
    }

    protected Message createStockMessage(String stock, Session session) throws JMSException {
        Double value = LAST_PRICES.get(stock);
        if (value == null) {
            value = new Double(Math.random() * 100);
        }

        // lets mutate the value by some percentage
        double oldPrice = value.doubleValue();
        value = new Double(mutatePrice(oldPrice));
        LAST_PRICES.put(stock, value);
        double price = value.doubleValue();

        double offer = price * 1.001;

        boolean up = (price > oldPrice);
        MapMessage message = session.createMapMessage();
        message.setString("stock", stock);
        message.setDouble("price", price);
        message.setDouble("offer", offer);
        message.setBoolean("up", up);
        return message;
    }

    protected double mutatePrice(double price) {
        double percentChange = (2 * Math.random() * MAX_DELTA_PERCENT) - MAX_DELTA_PERCENT;

        return price * (100 + percentChange) / 100;
    }

}
```

- [ ] Let's package the project

```
mvn package
```

- [ ] :rocket: Let's run the `Publisher` app in a separate :desktop_computer: Terminal

* using `tcp` protocol

```
mvn exec:java --define exec.mainClass=org.apache.activemq.book.ch4.openwire.Publisher --define exec.args="tcp://localhost:61616 CSCO ORCL"
```

* using `nio` protocol

```
mvn exec:java --define exec.mainClass=org.apache.activemq.book.ch4.openwire.Publisher --define exec.args="nio://localhost:61616 CSCO ORCL"
```


# [:back: ](../../../../../../../../README.md) Return to `ch4`
