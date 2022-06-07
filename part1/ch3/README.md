# Chapter :three:


- [ ] Open [VSC](https://code.visualstudio.com)

```
code .
```

- [ ] 2 coding examples

| component | Source Code |
|-----------|-------------|
| Queue     | [jobs](org/apache/activemq/book/ch3/jobs) |
| Topic     | [portfolio](org/apache/activemq/book/ch3/portfolio) |


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
-classpath target/ch3-1.0-SNAPSHOT.jar:$HOME/.m2/repository/javax/jms/javax.jms-api/2.0.1/javax.jms-api-2.0.1.jar:$HOME/.m2/repository/org/apache/activemq/activemq-all/5.16.2/activemq-all-5.16.2.jar \
org.apache.activemq.book.ch3.jobs.Producer 
```

