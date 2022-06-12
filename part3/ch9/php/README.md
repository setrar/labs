

```
composer require stomp-php/stomp-php
```

```php
<?php

require_once('Stomp.php');

$stomp = new Stomp('tcp://localhost:61613');
$stomp->connect();

$stomp->send('/queue/test', 'test');
echo "Sent message with body 'test'\n";

$stomp->subscribe('/queue/test');

$message = $stomp->readFrame();

// do what you want with the message
if ($message !== null) {
    echo "Received message with body '$message->body'\n";
    $stomp->ack($message);
} else {
    echo "Failed to receive a message\n";
}

$stomp->disconnect();
```

# References

https://github.com/stomp-php/stomp-php/wiki/First-example
