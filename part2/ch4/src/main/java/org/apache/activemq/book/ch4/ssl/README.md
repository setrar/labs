

```
cd ${ACTIVEMQ_HOME}
```

```
${ACTIVEMQ_HOME}/bin/activemq console xbean:examples/conf/activemq-demo.xml 
```


```
mvn \
 --define javax.net.ssl.keyStore=${ACTIVEMQ_HOME}/conf/client.ks \
 --define javax.net.ssl.keyStorePassword=password \
 --define javax.net.ssl.trustStore=${ACTIVEMQ_HOME}/conf/client.ts \
 exec:java --define exec.mainClass=org.apache.activemq.book.ch4.Consumer \
           --define exec.args="ssl://localhost:61617 CSCO ORCL"
```

```
mvn \
 --define javax.net.ssl.keyStore=${ACTIVEMQ_HOME}/conf/client.ks \
 --define javax.net.ssl.keyStorePassword=password \
 --define javax.net.ssl.trustStore=${ACTIVEMQ_HOME}/conf/client.ts \
 exec:java --define exec.mainClass=org.apache.activemq.book.ch4.Publisher \
           --define exec.args="ssl://localhost:61617 CSCO ORCL"
```


<img src="../../../../../../../images/ssl-connector.png" width= heigth= /> </img>

## :warning: ERROR

```
ERROR | Could not set property host on SSLSocket[hostname=null, port=0, Session(1654912974021|SSL_NULL_WITH_NULL_NULL)]
java.lang.reflect.InaccessibleObjectException: Unable to make public void sun.security.ssl.SSLSocketImpl.setHost(java.lang.String) accessible: module java.base does not "exports sun.security.ssl" to unnamed module @4ab83a82
        at java.base/java.lang.reflect.AccessibleObject.checkCanSetAccessible(AccessibleObject.java:354)
        at java.base/java.lang.reflect.AccessibleObject.checkCanSetAccessible(AccessibleObject.java:297)
        at java.base/java.lang.reflect.Method.checkCanSetAccessible(Method.java:199)
        at java.base/java.lang.reflect.Method.setAccessible(Method.java:193)
        at org.apache.activemq.util.IntrospectionSupport.setProperty(IntrospectionSupport.java:179)
        at org.apache.activemq.util.IntrospectionSupport.setProperties(IntrospectionSupport.java:155)
        at org.apache.activemq.util.IntrospectionSupport.setProperties(IntrospectionSupport.java:140)
        at org.apache.activemq.transport.tcp.SslTransport.<init>(SslTransport.java:81)
        at org.apache.activemq.transport.tcp.SslTransportFactory.createTransport(SslTransportFactory.java:122)
        at org.apache.activemq.transport.TransportFactory.doConnect(TransportFactory.java:120)
        at org.apache.activemq.transport.TransportFactory.connect(TransportFactory.java:65)
        at org.apache.activemq.ActiveMQConnectionFactory.createTransport(ActiveMQConnectionFactory.java:331)
        at org.apache.activemq.ActiveMQConnectionFactory.createActiveMQConnection(ActiveMQConnectionFactory.java:346)
        at org.apache.activemq.ActiveMQConnectionFactory.createActiveMQConnection(ActiveMQConnectionFactory.java:304)
        at org.apache.activemq.ActiveMQConnectionFactory.createConnection(ActiveMQConnectionFactory.java:244)
        at org.apache.activemq.book.ch4.Publisher.<init>(Publisher.java:32)
        at org.apache.activemq.book.ch4.Publisher.main(Publisher.java:51)
        at org.codehaus.mojo.exec.ExecJavaMojo$1.run(ExecJavaMojo.java:254)
        at java.base/java.lang.Thread.run(Thread.java:833)
```

# References

- [ ] [Java 16 SSL connection gives an error in the log](https://issues.apache.org/jira/browse/AMQ-8275?page=com.atlassian.jira.plugin.system.issuetabpanels%3Aall-tabpanel)

  JDK 11 support is coming in 5.17.0. This appears to be a module export problem

  module java.base does not "exports sun.security.ssl" to unnamed module
  
- [ ] [How do I use SSL?](https://activemq.apache.org/how-do-i-use-ssl)
