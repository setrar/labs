
```
${ACTIVEMQ_HOME}/bin/activemq console xbean:src/main/resources/org/apache/activemq/book/ch4/activemq-ssl.xml 
```

```
mvn \
 --define javax.net.ssl.keyStore=${ACTIVEMQ_HOME}/conf/client.ks \
 --define javax.net.ssl.keyStorePassword=password \
 --define javax.net.ssl.trustStore=${ACTIVEMQ_HOME}/conf/client.ts \
 exec:java --define exec.mainClass=org.apache.activemq.book.ch4.Publisher \
           --define exec.args="ssl://localhost:61617 CSCO ORCL
```
