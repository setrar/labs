# Sync


:bulb: in the `sync` folder

:round_pushpin: Add the `Server` Java Source Code

- [ ] use the `Server` Class as an example

```java
package org.apache.activemq.book.ch7.sync;

import javax.jms.Connection;
import javax.jms.DeliveryMode;
import javax.jms.Destination;
import javax.jms.JMSException;
import javax.jms.Message;
import javax.jms.MessageConsumer;
import javax.jms.MessageListener;
import javax.jms.MessageProducer;
import javax.jms.Session;
import javax.jms.TextMessage;

import org.apache.activemq.ActiveMQConnectionFactory;
import org.apache.activemq.broker.BrokerService;

public class Server implements MessageListener {

	private String brokerUrl = "tcp://0.0.0.0:61616";
	private String requestQueue = "requests";
	
	private BrokerService broker;
	private Session session;
	private MessageProducer producer;
	private MessageConsumer consumer;
	

	public void start() throws Exception {
		createBroker();
		setupConsumer();
	}

	private void createBroker() throws Exception {
        broker = new BrokerService();
        broker.setPersistent(false);
        broker.setUseJmx(false);
        broker.addConnector(brokerUrl);
        broker.start();		
	}

	private void setupConsumer() throws JMSException {
		ActiveMQConnectionFactory connectionFactory = new ActiveMQConnectionFactory(brokerUrl);
		
		Connection connection;
		connection = connectionFactory.createConnection();
		connection.start();
		session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
		Destination adminQueue = session.createQueue(requestQueue);

		producer = session.createProducer(null);
		producer.setDeliveryMode(DeliveryMode.NON_PERSISTENT);

		consumer = session.createConsumer(adminQueue);
		consumer.setMessageListener(this);
	}
	
	public void stop() throws Exception {
		producer.close();
		consumer.close();
		session.close();
		broker.stop();
	}
	
	public void onMessage(Message message) {
        try {
            TextMessage response = this.session.createTextMessage();
            if (message instanceof TextMessage) {
                TextMessage txtMsg = (TextMessage) message;
                String messageText = txtMsg.getText();
                response.setText(handleRequest(messageText));
            }

            response.setJMSCorrelationID(message.getJMSCorrelationID());

            producer.send(message.getJMSReplyTo(), response);
        } catch (JMSException e) {
            e.printStackTrace();
        }
	}
	
	public String handleRequest(String messageText) {
		return "Response to '" + messageText + "'";
	}
	
	public static void main(String[] args) throws Exception {
		Server server = new Server();
		server.start();
		
		System.out.println();
		System.out.println("Press any key to stop the server");
		System.out.println();
		
		System.in.read();
		
		server.stop();
	}

}
```

:round_pushpin: Add the `Client` Java Source Code

- [ ] use the `Client` Class as an example


```java
package org.apache.activemq.book.ch7.sync;

import java.util.UUID;

import javax.jms.Connection;
import javax.jms.DeliveryMode;
import javax.jms.Destination;
import javax.jms.JMSException;
import javax.jms.Message;
import javax.jms.MessageConsumer;
import javax.jms.MessageListener;
import javax.jms.MessageProducer;
import javax.jms.Session;
import javax.jms.TextMessage;

import org.apache.activemq.ActiveMQConnectionFactory;

public class Client implements MessageListener {

	private String brokerUrl = "tcp://0.0.0.0:61616";
	private String requestQueue = "requests";
	
	Connection connection;
	private Session session;
	private MessageProducer producer;
	private MessageConsumer consumer;
	
	private Destination tempDest;
	
	public void start() throws JMSException {
		ActiveMQConnectionFactory connectionFactory = new ActiveMQConnectionFactory(
				brokerUrl);
		connection = connectionFactory.createConnection();
		connection.start();
		session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
		Destination adminQueue = session.createQueue(requestQueue);

		producer = session.createProducer(adminQueue);
		producer.setDeliveryMode(DeliveryMode.NON_PERSISTENT);

		tempDest = session.createTemporaryQueue();
		consumer = session.createConsumer(tempDest);

		consumer.setMessageListener(this);
	}

	public void stop() throws JMSException {
		producer.close();
		consumer.close();
		session.close();
		connection.close();
	}
	
	public void request(String request) throws JMSException {
		System.out.println("Requesting: " + request);
		TextMessage txtMessage = session.createTextMessage();
		txtMessage.setText(request);

		txtMessage.setJMSReplyTo(tempDest);

		String correlationId = UUID.randomUUID().toString();
		txtMessage.setJMSCorrelationID(correlationId);
		this.producer.send(txtMessage);
	}

	public void onMessage(Message message) {
		try {
			System.out.println("Received response for: "
					+ ((TextMessage) message).getText());
		} catch (JMSException e) {
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) throws Exception {
		Client client = new Client();
		client.start();
		int i = 0;
		while (i++ < 10) {
			client.request("REQUEST-" + i);
		}
		Thread.sleep(3000); //wait for replies
		client.stop();
	}

}
```


- [ ] Let's package the project

```
mvn package
```

- [ ] :rocket: Let's run the `Server` app in a separate :desktop_computer: Terminal

```
mvn exec:java --define exec.mainClass=org.apache.activemq.book.ch7.sync.Server 
```


- [ ] :rocket:  Start up the client for the request/reply example


```
mvn exec:java --define exec.mainClass=org.apache.activemq.book.ch7.sync.Client 
```
> Returns
```
Requesting: REQUEST-1
Requesting: REQUEST-2
Requesting: REQUEST-3
Requesting: REQUEST-4
Requesting: REQUEST-5
Requesting: REQUEST-6
Requesting: REQUEST-7
Requesting: REQUEST-8
Requesting: REQUEST-9
Requesting: REQUEST-10
Received response for: Response to 'REQUEST-1'
Received response for: Response to 'REQUEST-2'
Received response for: Response to 'REQUEST-3'
Received response for: Response to 'REQUEST-4'
Received response for: Response to 'REQUEST-5'
Received response for: Response to 'REQUEST-6'
Received response for: Response to 'REQUEST-7'
Received response for: Response to 'REQUEST-8'
Received response for: Response to 'REQUEST-9'
Received response for: Response to 'REQUEST-10' 
```

# [:back: ](../../../../../../../../README.md) Return to `ch7`


