# ch:six: :heavy_minus_sign: Securing ActiveMQ

## :dash: plug-ins

Two `plug-ins` are available in ActiveMQ to authenticate users:

* Simple authentication plug-in— Handles credentials directly in the XML configuration file or in a properties file
* JAAS authentication plug-in— Implements the JAAS API and provides a more powerful and customizable authentication solution

## :a: Configuring the simple authentication plug-in

- [ ] Add the `plug-in` to the ActiveMQ configuration file

```xml
        <plugins>
            <simpleAuthenticationPlugin>
                <!-- Four authentication users with their groups -->
                <users>
                    <authenticationUser username="admin" password="password" groups="admins,publishers,consumers"/>
                    <authenticationUser username="publisher" password="password" groups="publishers,consumers"/>
                    <authenticationUser username="consumer" password="password" groups="consumers"/>
                    <authenticationUser username="guest" password="password" groups="guests"/>
                </users>
            </simpleAuthenticationPlugin>
        </plugins>
```

- [ ] Start the broker

```
${ACTIVEMQ_HOME}/bin/activemq console \
    xbean:src/main/resources/org/apache/activemq/book/ch6/activemq-simple.xml
```

- [ ] Test the authentication

:bulb: Launch the app from ch:four:

```
mvn exec:java \
   --define exec.mainClass=org.apache.activemq.book.ch4.Publisher \
   --define exec.args="tcp://localhost:61616 CSCO ORCL"
```
> Returns
```
[WARNING]
javax.jms.JMSSecurityException: User name [null] or password is invalid.
```

```java
private String username = "publisher";
private String password = "password";

public Publisher() throws JMSException {
    factory = new ActiveMQConnectionFactory(brokerURL);
    connection = factory.createConnection(username, password);
    connection.start();
    session = connection.createSession(false,
    Session.AUTO_ACKNOWLEDGE);
    producer = session.createProducer(null);
}
```
