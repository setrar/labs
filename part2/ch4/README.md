# Chapter :four:


- [ ] Open [VSC](https://code.visualstudio.com)

```
code .
```

- [ ] 1 coding example

| component | Source Code |  Schematic |
|-----------|-------------|--|
| Topic     | [ch4](src/main/java/org/apache/activemq/book/ch4) | <img src="../../images/stock-portfolio-example.png" width=528 height=237  /> </img> |

# [:back: ](..) Return to Part:one:

# References

- [ ] External `Maven` Libraries used for this chapter

| Maven Libraries                                                                                                       |
|-----------------------------------------------------------------------------------------------------------------------|
| [javax.jms/javax.jms-api/2.0.1](https://mvnrepository.com/artifact/javax.jms/javax.jms-api/2.0.1)                     |
| [org.apache.activemq/activemq-all/5.16.2](https://mvnrepository.com/artifact/org.apache.activemq/activemq-all/5.16.2) |

- [ ] :steam_locomotive: Running the app using `java` binary

:bulb: observe the `-classpath` argument which is extra long

```
java \
-classpath target/ch4-1.0-SNAPSHOT.jar:$HOME/.m2/repository/javax/jms/javax.jms-api/2.0.1/javax.jms-api-2.0.1.jar:$HOME/.m2/repository/org/apache/activemq/activemq-all/5.16.2/activemq-all-5.16.2.jar \
org.apache.activemq.book.ch4.jobs.Publisher 
```

