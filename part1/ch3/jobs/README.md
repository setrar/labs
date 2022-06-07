## :a: jobs

:bulb: in the `jobs` folder

:round_pushpin: Add the `Producer` Java Source Code

- [ ] use the Producer Class as an example

```java
package org.apache.activemq.book.ch3.jobs;

import javax.jms.Connection;
import javax.jms.ConnectionFactory;
import javax.jms.Destination;
import javax.jms.JMSException;
import javax.jms.Message;
import javax.jms.MessageProducer;
import javax.jms.ObjectMessage;
import javax.jms.Session;

import org.apache.activemq.ActiveMQConnectionFactory;

public class Producer {

    private static String brokerURL = "tcp://localhost:61616";
    private static transient ConnectionFactory factory;
    private transient Connection connection;
    private transient Session session;
    private transient MessageProducer producer;
    
    private static int count = 10;
    private static int total;
    private static int id = 1000000;
    
    private String jobs[] = new String[]{"suspend", "delete"};
    
    public Producer() throws JMSException {
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
    	Producer producer = new Producer();
        while (total < 1000) {
            for (int i = 0; i < count; i++) {
                producer.sendMessage();
            }
            total += count;
            System.out.println("Sent '" + count + "' of '" + total + "' job messages");
            try {
              Thread.sleep(1000);
            } catch (InterruptedException x) {
            }
        }
        producer.close();

    }
	
    public void sendMessage() throws JMSException {
        int idx = 0;
        while (true) {
            idx = (int)Math.round(jobs.length * Math.random());
            if (idx < jobs.length) {
                break;
            }
        }
        String job = jobs[idx];
        Destination destination = session.createQueue("JOBS." + job);
        Message message = session.createObjectMessage(id++);
        System.out.println("Sending: id: " + ((ObjectMessage)message).getObject() + " on queue: " + destination);
        producer.send(destination, message);
    }	

}
```

- [ ] Let's package the project

```
mvn package
```

- [ ] :rocket: Let's run the app using `Maven` executable plugin `exec:<language>` by `defining` the `exec.mainClass` system property (or argument)

```
mvn exec:java --define exec.mainClass=org.apache.activemq.book.ch3.jobs.Producer
```

:round_pushpin: Add the `Consumer` Java Source Code

- [ ] use the `Consumer` Class as an example

```java
package org.apache.activemq.book.ch3.jobs;

import javax.jms.Connection;
import javax.jms.ConnectionFactory;
import javax.jms.Destination;
import javax.jms.JMSException;
import javax.jms.MessageConsumer;
import javax.jms.Session;

import org.apache.activemq.ActiveMQConnectionFactory;

public class Consumer {

    private static String brokerURL = "tcp://localhost:61616";
    private static transient ConnectionFactory factory;
    private transient Connection connection;
    private transient Session session;
    
    private String jobs[] = new String[]{"suspend", "delete"};
    
    public Consumer() throws JMSException {
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
    	Consumer consumer = new Consumer();
    	for (String job : consumer.jobs) {
    		Destination destination = consumer.getSession().createQueue("JOBS." + job);
    		MessageConsumer messageConsumer = consumer.getSession().createConsumer(destination);
    		messageConsumer.setMessageListener(new Listener(job));
    	}
    }
	
    public Session getSession() {
        return session;
    }


}
```

- [ ] you need the `Listener` Class to retrieve your message

```java
package org.apache.activemq.book.ch3.jobs;

import javax.jms.Message;
import javax.jms.MessageListener;
import javax.jms.ObjectMessage;

public class Listener implements MessageListener {

	private String job;
	
	public Listener(String job) {
		this.job = job;
	}

	public void onMessage(Message message) {
		try {
			//do something here
			System.out.println(job + " id:" + ((ObjectMessage)message).getObject());
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}
```

