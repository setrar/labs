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

## :b: HellowWorldScala example from [Hello World Scala in the Cloud With Spring](https://dzone.com/articles/spring-scala-cloud-psh)

- [ ] Create the maven `helloworldScala` project

```
mvn archetype:generate \
    -DgroupId=com.valiha.app \
    -DartifactId=helloworldScala \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DarchetypeVersion=1.4 \
    -DinteractiveMode=false
```


# References

- [ ] [ActiveMQ Performance Testing](https://www.javacodegeeks.com/2018/09/activemq-performance-testing.html)



