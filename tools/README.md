# :toolbox: Tools


Tutorial on how to setup a `Windows` machine to use the ActiveMQ lab

## :warning: Prerequisites

This lab uses :copyright: Microsoft Windows Machine



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

:rocket: running the app using `Maven` executable plugin `exec:<language>` along by `defining` its argument `exec.mainClass`

```
mvn exec:java --define exec.mainClass=com.valiha.app.App 
```

:steam_locomotive: Running the app using `java` binary

:bulb: observe the `-classpath` argument which may be extra long

```
java -classpath target/helloworld-1.0-SNAPSHOT.jar com.valiha.app.App 
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


