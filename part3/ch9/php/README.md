```php
<?php
require __DIR__ . '/../vendor/autoload.php';
/**
 *
 * Copyright (C) 2009 Progress Software, Inc. All rights reserved.
 * http://fusesource.com
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

use Stomp\Client;
use Stomp\StatefulStomp;
use Stomp\Transport\Message;

// make a connection
$stomp = new StatefulStomp(
    new Client('failover://(tcp://localhost:61614,ssl://localhost:61612,tcp://localhost:61613)?randomize=false')
);

// send a message to the queue
$stomp->send('/queue/test', new Message('test'));
echo "Sent message with body 'test'\n";
// subscribe to the queue
$stomp->subscribe('/queue/test', null, 'client-individual');
// receive a message from the queue
$msg = $stomp->read();

// do what you want with the message
if ($msg != null) {
    echo "Received message with body '$msg->body'\n";
    // mark the message as received in the queue
    $stomp->ack($msg);
} else {
    echo "Failed to receive a message\n";
}

$stomp->unsubscribe();
```



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
https://github.com/stomp-php/stomp-php-examples/blob/support/version-4/src/connectivity.php
