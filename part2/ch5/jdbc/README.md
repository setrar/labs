# ch:five:  The JDBC message store


## :a: MySQL Docker Installation 

### :round_pushpin: Creating and Accessing the `MySQL` Container 

https://hub.docker.com/_/mysql/

- [ ] Creating the Container

```
docker container run --name some-mysql --env MYSQL_ROOT_PASSWORD=activemq --publish 3306:3306 --detach mysql:latest
```

- [ ] Accessing the Container

```
docker container exec --interactive --tty some-mysql bash
```


> the input device is not a TTY.  If you are using mintty, try prefixing the command with 'winpty' 

:bulb: Add `winpty` in front of the command. To insert characters at the beginning of the command type `CTRL+A` on your keyboard 

### :round_pushpin: `MySQL` Database Settings

- [ ] launch the MySQL CLI (Command Level Interface) inside the container

:bulb: The container's prompt should be the :hash: character

```
mysql --user root --password
```

:facepalm: `password` is the `root` password

- [ ] In the MySQL CLI, create the `activemq` database

:bulb: The MySQL's CLI prompt should be `mysql>`

```
CREATE DATABASE activemq;
```

- [ ] create the `activemq` MySQL user (along with password)


* user and password

```
CREATE USER 'activemq'@'%' IDENTIFIED BY 'activemq';
```

* user privileges to access the `activemq` DB

```
GRANT ALL ON activemq.* TO 'activemq'@'%';
```

- [ ] Immediate activation

```
flush privileges;
```

- [ ] Exiting from the MySQL CLI and container

```
exit
```

## :b: Activate your ActiveMQ broker using the MySQL Storage parameters

### :round_pushpin: run the Broker

In the `ch5` directory

```
${ACTIVEMQ_HOME}/bin/activemq console xbean:jdbc/conf/activemq.xml
```

- [ ] The configuration file

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

```xml
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

   <!-- Allows accessing the server log -->
    <bean id="logQuery" class="io.fabric8.insight.log.log4j.Log4jLogQuery"
          lazy-init="false" scope="singleton"
          init-method="start" destroy-method="stop">
    </bean>

    <!--
        The <broker> element is used to configure the ActiveMQ broker.
    -->
    <broker xmlns="http://activemq.apache.org/schema/core" brokerName="localhost" dataDirectory="${activemq.data}">

         <destinationPolicy>
            <policyMap>
              <policyEntries>
                <policyEntry topic=">" >
                    <!-- The constantPendingMessageLimitStrategy is used to prevent
                         slow topic consumers to block producers and affect other consumers
                         by limiting the number of messages that are retained
                         For more information, see:

                         http://activemq.apache.org/slow-consumer-handling.html

                    -->
                  <pendingMessageLimitStrategy>
                    <constantPendingMessageLimitStrategy limit="1000"/>
                  </pendingMessageLimitStrategy>
                </policyEntry>
              </policyEntries>
            </policyMap>
        </destinationPolicy>


        <!--
            The managementContext is used to configure how ActiveMQ is exposed in
            JMX. By default, ActiveMQ uses the MBean server that is started by
            the JVM. For more information, see:

            http://activemq.apache.org/jmx.html
        -->
        <managementContext>
            <managementContext createConnector="false"/>
        </managementContext>
         <!--
            Configure message persistence for the broker. The default persistence
            mechanism is the KahaDB store (identified by the kahaDB tag).
            For more information, see:

            http://activemq.apache.org/persistence.html
        -->
        <persistenceAdapter>
            <!--
            <kahaDB directory="${activemq.data}/kahadb"/>
            -->
            <jdbcPersistenceAdapter dataDirectory="${activemq.data}" dataSource="#mysql-ds"/>
        </persistenceAdapter>


          <!--
            The systemUsage controls the maximum amount of space the broker will
            use before disabling caching and/or slowing down producers. For more information, see:
            http://activemq.apache.org/producer-flow-control.html
          -->
          <systemUsage>
            <systemUsage>
                <memoryUsage>
                    <memoryUsage percentOfJvmHeap="70" />
                </memoryUsage>
                <storeUsage>
                    <storeUsage limit="100 gb"/>
                </storeUsage>
                <tempUsage>
                    <tempUsage limit="50 gb"/>
                </tempUsage>
            </systemUsage>
        </systemUsage>

         <!--
            The transport connectors expose ActiveMQ over a given protocol to
            clients and other brokers. For more information, see:

            http://activemq.apache.org/configuring-transports.html
        -->
        <transportConnectors>
            <!-- DOS protection, limit concurrent connections to 1000 and frame size to 100MB -->
            <transportConnector name="openwire" uri="tcp://0.0.0.0:61616?maximumConnections=1000&amp;wireFormat.maxFrameSize=104857600"/>
            <transportConnector name="amqp" uri="amqp://0.0.0.0:5672?maximumConnections=1000&amp;wireFormat.maxFrameSize=104857600"/>
            <transportConnector name="stomp" uri="stomp://0.0.0.0:61613?maximumConnections=1000&amp;wireFormat.maxFrameSize=104857600"/>
            <transportConnector name="mqtt" uri="mqtt://0.0.0.0:1883?maximumConnections=1000&amp;wireFormat.maxFrameSize=104857600"/>
            <transportConnector name="ws" uri="ws://0.0.0.0:61614?maximumConnections=1000&amp;wireFormat.maxFrameSize=104857600"/>
            <transportConnector name="ssl" uri="ssl://localhost:61617?trace=true" />
            <transportConnector name="http" uri="http://localhost:8080?trace=true" />
        </transportConnectors>

        <!-- destroy the spring context on shutdown to stop jetty -->
        <shutdownHooks>
            <bean xmlns="http://www.springframework.org/schema/beans" class="org.apache.activemq.hooks.SpringContextHook" />
        </shutdownHooks>

    </broker>

    <!--
        Enable web consoles, REST and Ajax APIs and demos
        The web consoles requires by default login, you can disable this in the jetty.xml file

        Take a look at ${ACTIVEMQ_HOME}/conf/jetty.xml for more details
    -->
    <import resource="jetty.xml"/>

        <!--
        See more database locker options at http://activemq.apache.org/pluggable-storage-lockers.html
    -->
  
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

```xml
    <persistenceFactory>
      <journalPersistenceAdapterFactory
       journalLogFiles="4"
       journalLogFileSize="32768"
       useJournal="true"
       useQuickJournal="true"
       dataSource="#derby-ds"
       dataDirectory="activemq-data" />
    </persistenceFactory>
```

- [ ] References

https://activemq.apache.org/leveldb-store.html

