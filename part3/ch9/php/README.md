# Stomp - PHP Example

## :gear: Install `php` and `composer`

:point_right: [Install](installation) - (Already preinstalled, no action needed)

## :a: Install Stomp

:point_right: [Stomp](Stomp)

## :b: Create the PHP source file called `consumer.php`

- [ ] `consumer.php` content

```php
<?php
require __DIR__ . '/Stomp/vendor/autoload.php';

use Stomp\Client;
use Stomp\SimpleStomp;

// make a connection
$stomp = new SimpleStomp(new Client('tcp://localhost:61613'));

$stomp->subscribe('/topic/STOCKS.IONA', 'binary-sub-test', 'client-individual');
$stomp->subscribe('/topic/STOCKS.JAVA', 'binary-sub-test', 'client-individual');

$i = 0;
while ($i++ < 100) {
   $frame = $stomp->read();
    // extract
    if ($frame != null) {
        $xml = new SimpleXMLElement($frame->body);
        echo $xml->attributes()->name
           . "\t" . number_format(floatval($xml->price),2)
           . "\t" . number_format(floatval($xml->offer),2)
           . "\t" . ($xml->up == "true"?"up":"down") . "\n";

        // mark the message as received in the queue
        $stomp->ack($frame);
    } else {
        echo "Failed to receive a message\n";
    }
}

$stomp->unsubscribe('/topic/STOCKS.IONA', 'binary-sub-test');
$stomp->unsubscribe('/topic/STOCKS.JAVA', 'binary-sub-test');
```

- [ ] Run the php source code

```
php consumer.php
```

- [ ] Knonw issue

:warning: `PHP Fatal error:  Uncaught Stomp\Exception\ErrorFrameException: Error "No subscription matched." `

## :o: Test Stomp Connection

- [ ] Run the Maven Exec Java of ch:nine: in a different window Terminal

```
mvn exec:java --define exec.mainClass=org.apache.activemq.book.ch9.Publisher \
              --define exec.args="stomp://localhost:1883 IONA JAVA" 
```

# References

- [ ] [Stomp PHP - Examples](https://github.com/stomp-php/stomp-php-examples)
