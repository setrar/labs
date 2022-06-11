# 

Two plug-ins are available in ActiveMQ to authenticate users:

* Simple authentication plug-in— Handles credentials directly in the XML configuration file or in a properties file
* JAAS authentication plug-in— Implements the JAAS API and provides a more powerful and customizable authentication solution

```
${ACTIVEMQ_HOME}/bin/activemq console \
    xbean:src/main/resources/org/apache/activemq/book/ch6/activemq-simple.xml
```
