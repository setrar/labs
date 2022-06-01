# ActiveMQ



## :a: HelloWorld example from [Maven in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)

- [ ] Create the maven `helloworld` project

```
mvn archetype:generate \
    -DgroupId=com.valiha.app \
    -DartifactId=helloworld \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DarchetypeVersion=1.4 \
    -DinteractiveMode=false
```

- [ ] Create the java package (along with compiling)

```
mvn package
```

- [ ] Run the app

```
java -classpath target/helloworld-1.0-SNAPSHOT.jar com.valiha.app.App 
```

```
mvn exec:java --define execMainClass=com.valiha.app.App 
```



## :b: HellowWorldScala example from [Hello World Scala in the Cloud With Spring](https://dzone.com/articles/spring-scala-cloud-psh)

- [ ] Create the maven `helloworldScala` project

```
mvn archetype:generate \
    -DgroupId=com.valiha.app \
    -DartifactId=helloworldscala \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DarchetypeVersion=1.4 \
    -DinteractiveMode=false
```

```
mvn spring-boot:run
```

```
docker run --name some-mongo --detach mongo
```


# References

- [ ] [ActiveMQ Performance Testing](https://www.javacodegeeks.com/2018/09/activemq-performance-testing.html)
- [ ] [REST with Spring Tutorial](https://www.baeldung.com/rest-with-spring-series)
- [ ] [Spring MVC and Scala for Platform.sh](https://github.com/platformsh-examples/scala)
- [ ] [Create an ActiveMQ image and push it to your own docker hub account !](https://medium.com/@bilal.asif.97/create-an-activemq-image-and-push-it-to-your-own-docker-hub-account-516a05eba10a)

- [ ] [Version :five: Getting Started](https://activemq.apache.org/version-5-getting-started.html)

```
 netstat -an|grep 61616
```
> Return
```
  TCP    0.0.0.0:61616          0.0.0.0:0              LISTENING
  TCP    [::]:61616             [::]:0                 LISTENING
  TCP    [::1]:61616            [::]:0                 LISTENING
```

- [ ] [ActiveMQ in Action](https://www.manning.com/books/activemq-in-action)

* about the reader

  This book requires a working knowledge of Java, but no previous experience with ActiveMQ or other message brokers is needed.

* about the author

  Bruce Snyder is a co-founder of Apache Geronimo, a committer for ActiveMQ, Camel, and ServiceMix, and a member of various JCP expert groups. Dejan Bosanac is an ActiveMQ committer. Rob Davies is a co-founder of ActiveMQ, ServiceMix, and Camel.

- [ ] [ActiveMQ 5.16.2 Release](https://activemq.apache.org/activemq-5016002-release)
