# 

Two plug-ins are available in ActiveMQ to authenticate users:

* Simple authentication plug-in— Handles credentials directly in the XML configuration file or in a properties file
* JAAS authentication plug-in— Implements the JAAS API and provides a more powerful and customizable authentication solution

## :a: Simple

```xml
        <plugins>
            <simpleAuthenticationPlugin>
                <users>
                    <authenticationUser username="admin" password="password" groups="admins,publishers,consumers"/>
                    <authenticationUser username="publisher" password="password" groups="publishers,consumers"/>
                    <authenticationUser username="consumer" password="password" groups="consumers"/>
                    <authenticationUser username="guest" password="password" groups="guests"/>
                </users>
            </simpleAuthenticationPlugin>
        </plugins>
```

```
${ACTIVEMQ_HOME}/bin/activemq console \
    xbean:src/main/resources/org/apache/activemq/book/ch6/activemq-simple.xml
```
