# [ :desktop_computer: CLI - Command Line Interface - Tools and Reference](https://activemq.apache.org/activemq-command-line-tools-reference.html)

## :open_file_folder: Install Binary 

:round_pushpin:  Install Apache ActiveMQ by downloading the `activemq` distribution binary

```
curl -o apache-activemq-5.16.2-bin.zip https://archive.apache.org/dist/activemq/5.16.2/apache-activemq-5.16.2-bin.zip
```

- [ ] Extract the files and :point_right: go to the `activemq` folder

```
unzip apache-activemq-5.16.2-bin.zip && cd apache-activemq-5.16.2
```

:round_pushpin: Start ActiveMQ 

* Can also be started with `console` argument, CLI doesn't return, use `CTRL+C` to exit

```
bin/activemq start
```
> Returns
```
INFO: Using default configuration
      Configurations are loaded in the following order: /etc/default/activemq /c/Users/NobleProg/.activemqrc /c/Users/NobleProg/Developer/labs/activeMQ/apache-activemq-5.16.2//bin/env

INFO: Using java '/c/Users/NobleProg/.sdkman/candidates/java/current/bin/java'
INFO: Starting - inspect logfiles specified in logging.properties and log4j.properties to get details
INFO: pidfile created : '/c/Users/NobleProg/Developer/labs/activeMQ/apache-activemq-5.16.2//data/activemq.pid' (pid '2315')
```

- [ ] visit the admin console

http://localhost:8161/admin


- [ ] check if `activemq` is running on Ehternet Port `61616`

```
netstat -a | grep 61616
```
> Returns
```
  TCP    0.0.0.0:61616          brice-p7sl:0           LISTENING
  TCP    [::]:61616             brice-p7sl:0           LISTENING
```
 
- [ ] Done, shutdown the background running activemq app

```
bin/activemq stop
```

:round_pushpin: Run the `amqp`  Java Example

- [ ] Go to the example folder

```
cd examples/amqp/java
```

- [ ] Compile the project

```
mvn package
```

## :biohazard: Binary [examples](https://activemq.apache.org/examples)

- [ ] Run the listener first in a separate Terminal

```
java -classpath target/amqp-example-0.1-SNAPSHOT.jar example.Listener
```

- [ ] The Publisher should send messages, check back the Listener terminal

```
java -classpath target/amqp-example-0.1-SNAPSHOT.jar example.Publisher
```

## :tada: Start the WebDemo

```
bin/activemq console xbean:examples/conf/activemq-demo.xml 
```

# References

- [ ] [Using ActiveMQ > Getting Started](https://activemq.apache.org/getting-started)
- [ ] [ActiveMQ 5.16.2 Release](https://activemq.apache.org/activemq-5016002-release)

