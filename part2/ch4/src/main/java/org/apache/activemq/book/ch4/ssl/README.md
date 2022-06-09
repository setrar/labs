
```
${ACTIVEMQ_HOME}/bin/activemq console xbean:src/main/resources/org/apache/activemq/book/ch4/activemq-ssl.xml 
```

```
mvn \
 -Djavax.net.ssl.keyStore=${ACTIVEMQ_HOME}/conf/client.ks \
 -Djavax.net.ssl.keyStorePassword=password \
 -Djavax.net.ssl.trustStore=${ACTIVEMQ_HOME}/conf/client.ts \
 exec:java -Dexec.mainClass=org.apache.activemq.book.ch4.Publisher \
 -Dexec.args="ssl://localhost:61617 CSCO ORCL
```
