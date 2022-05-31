# :three:rd Chapter 

- [ ] Create the `maven` project

```
mvn archetype:generate \
    -DgroupId=org.apache.activemq.book.ch3 \
    -DartifactId=ch3 \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DarchetypeVersion=1.4 \
    -DinteractiveMode=false
```

- [ ] Navigate to the newly created `ch3` folder

```
cd ch3
```

* Add the `jobs` folder along with the `Producer` and `Consumer`

- [ ] Let's package the project

```
mvn package
```

- [ ] Let's run the `jobs` folder

```
java \
-classpath target/ch3-1.0-SNAPSHOT.jar:$HOME/.m2/repository/javax/jms/javax.jms-api/2.0.1/javax.jms-api-2.0.1.jar:$HOME/.m2/repository/org/apache/activemq/activemq-all/5.16.2/activemq-all-5.16.2.jar \
org.apache.activemq.book.ch3.jobs.Producer 
```

# [:back: ](..) Return to main page 

# References

- [ ] Library used for this chapter

| Maven Libraries |
|-----------------|
| [javax.jms/javax.jms-api/2.0.1](https://mvnrepository.com/artifact/javax.jms/javax.jms-api/2.0.1) |
| [org.apache.activemq/activemq-all/5.16.2](https://mvnrepository.com/artifact/org.apache.activemq/activemq-all/5.16.2) |

