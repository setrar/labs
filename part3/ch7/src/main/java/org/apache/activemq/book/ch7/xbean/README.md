# xbean


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

```java
package org.apache.activemq.book.ch7.xbean;

import java.util.ArrayList;
import java.util.List;

import org.apache.activemq.broker.BrokerPlugin;
import org.apache.activemq.broker.BrokerService;
import org.apache.activemq.security.AuthenticationUser;
import org.apache.activemq.security.SimpleAuthenticationPlugin;

public class Broker {

	public static void main(String[] args) throws Exception {
		BrokerService broker = new BrokerService();
		broker.setBrokerName("myBroker");
		broker.setDataDirectory("data/");
		
		SimpleAuthenticationPlugin authentication = new SimpleAuthenticationPlugin();
		
		List<AuthenticationUser> users = new ArrayList<AuthenticationUser>();
		users.add(new AuthenticationUser("admin", "password", "admins,publishers,consumers"));
		users.add(new AuthenticationUser("publisher", "password", "publishers,consumers"));
		users.add(new AuthenticationUser("consumer", "password", "consumers"));
		users.add(new AuthenticationUser("guest", "password", "guests"));
		authentication.setUsers(users);
		
		broker.setPlugins(new BrokerPlugin[]{authentication});
		
		/*JaasAuthenticationPlugin jaas = new JaasAuthenticationPlugin();
		jaas.setConfiguration("src/main/resources/org/apache/activemq/book/ch5/login.config");
		broker.setPlugins(new BrokerPlugin[]{jaas});*/		
		
		broker.addConnector("tcp://localhost:61616");
		
		broker.start();
		
		System.out.println();
		System.out.println("Press any key to stop the broker");
		System.out.println();
		
		System.in.read();
	}

}
```

```
mvn exec:java --define exec.mainClass=org.apache.activemq.book.ch7.xbean.Broker
```
> Returns
```
INFO | Using Persistence Adapter: KahaDBPersistenceAdapter[C:\Users\NobleProg\Developer\labs\part3\ch7\data\myBroker\KahaDB]
INFO | KahaDB is version 7
INFO | PListStore:[C:\Users\NobleProg\Developer\labs\part3\ch7\data\myBroker\tmp_storage] started
INFO | Apache ActiveMQ 5.16.2 (myBroker, ID:brice-p7sl-riiz-54546-1654989137770-0:1) is starting
INFO | Listening for connections at: tcp://kubernetes.docker.internal:61616
INFO | Connector tcp://kubernetes.docker.internal:61616 started
INFO | Apache ActiveMQ 5.16.2 (myBroker, ID:brice-p7sl-riiz-54546-1654989137770-0:1) started
INFO | For help or more information please see: http://activemq.apache.org
WARN | Store limit is 102400 mb (current store usage is 0 mb). The data directory: C:\Users\NobleProg\Developer\labs\part3\ch7\data\myBroker\KahaDB only has 15088 mb of usable space. - resetting to maximum available disk space: 15088 mb
WARN | Temporary Store limit is 51200 mb (current store usage is 0 mb). The data directory: C:\Users\NobleProg\Developer\labs\part3\ch7\data\myBroker only has 15088 mb of usable space. - resetting to maximum available disk space: 15088 mb
```
Press any key to stop the broker 
