# [ :desktop_computer: CLI - Command Line Interface - Tools and Reference](https://activemq.apache.org/activemq-command-line-tools-reference.html)

# Install Binary 

```
curl -o apache-activemq-5.16.2-bin.zip https://archive.apache.org/dist/activemq/5.16.2/apache-activemq-5.16.2-bin.zip 
```

```
unzip apache-activemq-5.16.2-bin.zip 
```

```
cd apache-activemq-5.16.2
```

```
bin/activemq start
```
> Return
```
INFO: Using default configuration
      Configurations are loaded in the following order: /etc/default/activemq /c/Users/NobleProg/.activemqrc /c/Users/NobleProg/Developer/labs/activeMQ/apache-activemq-5.16.2//bin/env

INFO: Using java '/c/Users/NobleProg/.sdkman/candidates/java/current/bin/java'
INFO: Starting - inspect logfiles specified in logging.properties and log4j.properties to get details
INFO: pidfile created : '/c/Users/NobleProg/Developer/labs/activeMQ/apache-activemq-5.16.2//data/activemq.pid' (pid '2315')
```

```
netstat -a | grep 61616
```
> Return
```
  TCP    0.0.0.0:61616          brice-p7sl:0           LISTENING
  TCP    [::]:61616             brice-p7sl:0           LISTENING
```
 

```
bin/activemq stop
```

## Binary [examples](https://activemq.apache.org/examples)

```
java -cp target/amqp-example-0.1-SNAPSHOT.jar example.Listener
```


```
java -cp target/amqp-example-0.1-SNAPSHOT.jar example.Publisher 
```

# References

- [ ] [Using ActiveMQ > Getting Started](https://activemq.apache.org/getting-started)
