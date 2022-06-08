# MOM - (Message Oriented Middleware) - Studying ActiveMQ

## :building_construction: Installing ActiveMQ `5.16.2`

Two ways to install ActiveMQ, one by using the official website and installing binaries, the other by creating our own Docker image to install the container using `Docker Desktop`

- [ ] Install the [ :bookmark: binary](bin) application

- [ ] Install through the [ :whale2: Docker](docker) container application

## :signal_strength: Monitoring


- [ ] WebConsole

 <img src="../images/activemq-web-consolepng" alt="hi" class="inline" width=780 />

- [ ] [JConsole](https://docs.oracle.com/en/java/javase/17/management/using-jconsole.html)

```
jconsole
```

 <img src="../images/jconsole-connection.png" alt="hi" class="inline" width=780 />

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
