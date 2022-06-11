# ch:six: :heavy_minus_sign: Securing ActiveMQ

## :dash: plug-ins

Two `plug-ins` are available in ActiveMQ to authenticate users:

* Simple authentication plug-in— Handles credentials directly in the XML configuration file or in a properties file
* JAAS authentication plug-in— Implements the JAAS API and provides a more powerful and customizable authentication solution

## :a: Configuring the simple authentication plug-in

:round_pushpin: Adding `authentication` to the broker

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

:round_pushpin: Enabling `authentication` programmatically

- [ ] Take the `Publisher.java` source code from ch:four:
- [ ] Do not forget to change its `Java` package name to ch:six:
- [ ] add the following code snippet to the Publisher `Constructor` Java `class`

* Snippet

```java
factory.createConnection(username, password);
```

* Publisher Class Constructor should look like tthis

```java
private String username = "publisher";
private String password = "password";

public Publisher() throws JMSException {
    factory = new ActiveMQConnectionFactory(brokerURL);
    connection = factory.createConnection(username, password);
    connection.start();
    session = connection.createSession(false,Session.AUTO_ACKNOWLEDGE);
    producer = session.createProducer(null);
}
```

- [ ] run the app

```
mvn exec:java \
   --define exec.mainClass=org.apache.activemq.book.ch6.Publisher \
   --define exec.args="tcp://localhost:61616 CSCO ORCL"
```

## :b: Configuring the [JAAS](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) plug-in

:3rd_place_medal: To be implemented if requested

# [:back: ](../../../../../../../../README.md) Return to `ch6`
