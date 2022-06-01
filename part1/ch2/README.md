# Chapter :two:

- [ ] Create the `maven` project

```
mvn archetype:generate \
    -DgroupId=org.apache.activemq.book.ch2 \
    -DartifactId=ch2 \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DarchetypeVersion=1.4 \
    -DinteractiveMode=false
```

- [ ] Navigate to the newly created `ch2` folder

```
cd ch2
```

- [ ] Open [VSC](https://code.visualstudio.com)

```
code .
```

## :a: jobs

- [ ] Create a new `jobs` folder

* Add the `jobs` folder along with the `Producer` and `Consumer`

- [ ] Let's package the project

```
mvn package
```

- [ ] :rocket: Let's run the app using `Maven` executable plugin `exec:<language>` by `defining` the `exec.mainClass` 

```
mvn exec:java --define exec.mainClass=org.apache.activemq.book.ch2.jobs.Producer
```


# [:back: ](..) Return to Part:one:

# References

- [ ] Library used for this chapter

| Maven Libraries                                                                                                       |
|-----------------------------------------------------------------------------------------------------------------------|
| [javax.jms/javax.jms-api/2.0.1](https://mvnrepository.com/artifact/javax.jms/javax.jms-api/2.0.1)                     |
| [org.apache.activemq/activemq-all/5.16.2](https://mvnrepository.com/artifact/org.apache.activemq/activemq-all/5.16.2) |

- [ ] :steam_locomotive: Running the app using `java` binary

:bulb: observe the `-classpath` argument which is extra long

```
java \
-classpath target/ch2-1.0-SNAPSHOT.jar:$HOME/.m2/repository/javax/jms/javax.jms-api/2.0.1/javax.jms-api-2.0.1.jar:$HOME/.m2/repository/org/apache/activemq/activemq-all/5.16.2/activemq-all-5.16.2.jar \
org.apache.activemq.book.ch2.jobs.Producer 
```

