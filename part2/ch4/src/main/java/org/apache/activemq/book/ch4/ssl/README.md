


- [ ] Maven Plugin

```xml
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
          <configuration>
            <argLine>--add-opens java.base/sun.security.ssl=ALL-UNNAMED</argLine>
          </configuration>
        </plugin>
```

```
vi ${ACTIVEMQ_HOME}/conf/activemq.xml
```

```xml
<transportConnectors>
 
   ...
   <transportConnector name="ssl" uri="ssl://localhost:61617?trace=true" 
</transportConnectors>
```
        
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

# References

- [ ] [Java 16 SSL connection gives an error in the log](https://issues.apache.org/jira/browse/AMQ-8275?page=com.atlassian.jira.plugin.system.issuetabpanels%3Aall-tabpanel)

  JDK 11 support is coming in 5.17.0. This appears to be a module export problem

  module java.base does not "exports sun.security.ssl" to unnamed module
  
- [ ] [How do I use SSL?](https://activemq.apache.org/how-do-i-use-ssl)
