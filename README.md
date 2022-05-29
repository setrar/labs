# labs

mvn archetype:generate \
    -DgroupId=org.apache.activemq.book.ch2.jobs \
    -DartifactId=activemq-in-action \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DarchetypeVersion=1.4 \
    -DinteractiveMode=false

```
java \
-classpath target/activemq-in-action-1.0-SNAPSHOT.jar:$HOME/.m2/repository/javax/jms/javax.jms-api/2.0.1/javax.jms-api-2.0.1.jar:$HOME/.m2/repository/org/apache/activemq/activemq-all/5.16.2/activemq-all-5.16.2.jar \
org.apache.activemq.book.ch2.jobs.Producer 
```
