# Status EXPERIMENTAL! Partial Working

# socketify
Socketify acts as a Proxy over diffrent NodeJS Only Libs to Port them to the Browser via calling them with socket.io

how that works?
var redis = require('redis')
socketify(anything that you could load via require)

socketify redis socket-redis => writes a socket-redis.js that has all methods of the original Object but it (Pollyfills) them so that they get send as messages with callback via socket.io

## Why?
I wanted to use some Modules directly in the Frontend Code and don't jump between backend and frontend Code for better maintainability of the overall code stack. As also Scaleability. It is Really a Amazing Project i think thats why i do it.

This is a Really Mighty tool as it can Pollyfill stuff like showed in the examples:

## Examples

### Redis
```
socketify redis socket-redis
//Server
var socket = io('address')
// Placing Listners on socket
var redisSocketMiddelware = require('/socket-redis/middelware.js')({ lib: redis, connection: socket })
```

All the Client Commands get Executed on the Server with the redis object of it and give directly the same reply as also he can read values from the original.
```
//Client
var socket = io('address')
var redis = require('/socket-redis/socket-redis.js')(socket)
    client = redis.createClient();
 
// if you'd like to select database 3, instead of 0 (default), call 
// client.select(3, function() { /* ... */ }); 
 
client.on("error", function (err) {
    console.log("Error " + err);
});
 
client.set("string key", "string val", redis.print);
client.hset("hash key", "hashtest 1", "some value", redis.print);
client.hset(["hash key", "hashtest 2", "some other value"], redis.print);
client.hkeys("hash key", function (err, replies) {
    console.log(replies.length + " replies:");
    replies.forEach(function (reply, i) {
        console.log("    " + i + ": " + reply);
    });
    client.quit();
});
```
### couchbase
### fs
### express
### memcached
### Anything :)
