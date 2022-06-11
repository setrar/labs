# ch:five:  The JDBC message store


## :a: MySQL Docker Installation 

### :round_pushpin: Creating and Accessing the `MySQL` Container 

https://hub.docker.com/_/mysql/

* Creating the Container

```
docker container run --name some-mysql --env MYSQL_ROOT_PASSWORD=activemq --publish 3306:3306 --detach mysql:latest
```

* Accessing the Container

```
docker container exec --interactive --tty some-mysql bash
```


### :round_pushpin: `MySQL` Database Settings

- [ ] launch the MySQL CLI (Command Level Interface) inside the container

:bulb: The container's prompt should be the :hash: character

```
mysql --user root --password
```


- [ ] In the MySQL CLI, create the `activemq` database

:bulb: The MySQL's CLI prompt should be `mysql>`

```
CREATE DATABASE activemq;
```

- [ ] create the `activemq` MySQL user (along with password)


* user and password

```
CREATE USER 'activemq'@'localhost' IDENTIFIED BY 'activemq';
```

* user privileges to access the `activemq` DB

```
GRANT ALL ON activemq.* TO 'activemq'@'localhost';
```

- [ ] Immediate activation

```
flush privileges;
```

## :b: Activate your ActiveMQ broker using the MySQL Storage parameters

```xml
<!--
    Use JDBC for message persistence
    For more information, see:

    http://activemq.apache.org/persistence.html

    You need to add Derby database to your classpath in order to make this example work.
    Download it from http://db.apache.org/derby/ and put it in the ${ACTIVEMQ_HOME}/lib/optional/ folder
    Optionally you can configure any other RDBM as shown below

    To run ActiveMQ with this configuration add xbean:examples/conf/activemq-jdbc.xml to your command

    e.g. $ bin/activemq console xbean:examples/conf/activemq-jdbc.xml
 -->
<beans
  xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
  http://activemq.apache.org/schema/core http://activemq.apache.org/schema/core/activemq-core.xsd">

  <!-- Allows us to use system properties as variables in this configuration file -->
  <bean class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
      <property name="locations">
          <value>file:${activemq.conf}/credentials.properties</value>
      </property>
  </bean>

  <broker useJmx="false" brokerName="jdbcBroker" xmlns="http://activemq.apache.org/schema/core">

    <!--
        See more database locker options at http://activemq.apache.org/pluggable-storage-lockers.html
    -->
    <persistenceAdapter>
       <jdbcPersistenceAdapter dataDirectory="${activemq.data}" dataSource="#mysql-ds"/>
    </persistenceAdapter>

    <transportConnectors>
       <transportConnector name="openwire" uri="tcp://0.0.0.0:61616"/>
    </transportConnectors>
  </broker>
  
  <!-- MySql DataSource Sample Setup -->
  <bean id="mysql-ds" class="org.apache.commons.dbcp2.BasicDataSource" destroy-method="close">
    <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
    <property name="url" value="jdbc:mysql://localhost/activemq?relaxAutoCommit=true"/>
    <property name="username" value="activemq"/>
    <property name="password" value="activemq"/>
    <property name="maxTotal" value="200"/>
    <property name="poolPreparedStatements" value="true"/>
  </bean>

</beans> 
```


- [ ] References

https://activemq.apache.org/leveldb-store.html

