# broker - Starting the broker using Java

:round_pushpin: Configure ActiveMQ with security plug-ins using XML

```xml
<broker xmlns="http://activemq.apache.org/schema/core" brokerName="myBroker" dataDirectory="${activemq.base}/data">

    <transportConnectors>
        <transportConnector name="openwire" uri="tcp://localhost:61616" />
    </transportConnectors>

    <plugins>
        <simpleAuthenticationPlugin>
            <users>
                <authenticationUser username="admin" password="password" groups="admins,publishers,consumers" />
                <authenticationUser username="publisher" password="password" groups="publishers,consumers" />
                <authenticationUser username="consumer" password="password" groups="consumers" />
                <authenticationUser username="guest" password="password" groups="guests" />
            </users>
        </simpleAuthenticationPlugin>
    </plugins>
</broker> 
```

:round_pushpin: Configure ActiveMQ with security plug-ins using Java


```java
package org.apache.activemq.book.ch7.broker;

import java.util.ArrayList;
import java.util.List;

import org.apache.activemq.broker.BrokerPlugin;
import org.apache.activemq.broker.BrokerService;
import org.apache.activemq.security.AuthenticationUser;
import org.apache.activemq.security.SimpleAuthenticationPlugin;

public class Broker {

	public static void main(String[] args) throws Exception {
		BrokerService broker = new BrokerService();
		
		// Initiate and configure the broker service
		broker.setBrokerName("myBroker");
		broker.setDataDirectory("data/");
		
		SimpleAuthenticationPlugin authentication = new SimpleAuthenticationPlugin();
		
		List<AuthenticationUser> users = new ArrayList<AuthenticationUser>();
		users.add(new AuthenticationUser("admin", "password", "admins,publishers,consumers"));
		users.add(new AuthenticationUser("publisher", "password", "publishers,consumers"));
		users.add(new AuthenticationUser("consumer", "password", "consumers"));
		users.add(new AuthenticationUser("guest", "password", "guests"));
		authentication.setUsers(users);
		
		// Add SimpleAuthentication Plugin
		broker.setPlugins(new BrokerPlugin[]{authentication});
		
		/*JaasAuthenticationPlugin jaas = new JaasAuthenticationPlugin();
		jaas.setConfiguration("src/main/resources/org/apache/activemq/book/ch5/login.config");
		broker.setPlugins(new BrokerPlugin[]{jaas});*/		
		
		// Add transport connector
		broker.addConnector("tcp://localhost:61616");
		
		// Start broker
		broker.start();
		
		System.out.println();
		System.out.println("Press any key to stop the broker");
		System.out.println();
		
		System.in.read();
	}

}
```

:bulb: Note

One important thing to note in Java listing above is that you should always add your plug-ins before connectors; otherwise they won’t be initialized. Also, any connectors added after the broker has been started won’t be properly started either.

:round_pushpin: Start the broker

```
mvn exec:java --define exec.mainClass=org.apache.activemq.book.ch7.broker.Broker
```
> Returns
```
21:53:44,025 |  INFO | Using Persistence Adapter: KahaDBPersistenceAdapter[C:\Users\NobleProg\Developer\labs\part3\ch7\data\myBroker\KahaDB]
21:53:44,262 |  INFO | KahaDB is version 7
21:53:45,254 |  INFO | PListStore:[C:\Users\NobleProg\Developer\labs\part3\ch7\data\myBroker\tmp_storage] started
21:53:45,531 |  INFO | Apache ActiveMQ 5.16.2 (myBroker, ID:brice-p7sl-riiz-49523-1654998825319-0:1) is starting
21:53:45,668 |  INFO | Listening for connections at: tcp://kubernetes.docker.internal:61616
21:53:45,669 |  INFO | Connector tcp://kubernetes.docker.internal:61616 started
21:53:45,670 |  INFO | Apache ActiveMQ 5.16.2 (myBroker, ID:brice-p7sl-riiz-49523-1654998825319-0:1) started
21:53:45,671 |  INFO | For help or more information please see: http://activemq.apache.org
21:53:45,679 |  WARN | Store limit is 102400 mb (current store usage is 0 mb). The data directory: C:\Users\NobleProg\Developer\labs\part3\ch7\data\myBroker\KahaDB only has 15041 mb of usable space. - resetting to maximum available disk space: 15041 mb
21:53:45,685 |  WARN | Temporary Store limit is 51200 mb (current store usage is 0 mb). The data directory: C:\Users\NobleProg\Developer\labs\part3\ch7\data\myBroker only has 15041 mb of usable space. - resetting to maximum available disk space: 15041 mb

Press any key to stop the broker
```

- [ ] Observe the File Message Storage :roll_of_paper:

```
find data/myBroker/KahaDB
```
> Returns
```
data/myBroker/KahaDB/
data/myBroker/KahaDB/db-1.log
data/myBroker/KahaDB/db.data
data/myBroker/KahaDB/db.redo
data/myBroker/KahaDB/lock
```

## :b: Test the Embedded Java Broker

- [ ] back to ch:six:

* Open a new Terminal Window :desktop_computer: 
* go back to ch:six: project `cd ${LABS}/part2/ch6`
* run the `Publisher` app

```
mvn exec:java \
   --define exec.mainClass=org.apache.activemq.book.ch6.Publisher \
   --define exec.args="tcp://localhost:61616 CSCO ORCL" 
``` 

# [:back: ](../../../../../../../../../README.md) Return to `ch7`
