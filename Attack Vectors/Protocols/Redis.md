# <h1 style="text-align:center">Remote Dictionary Server (Redis)</h1>

## Introduction
Redis is an open-source advanced NoSQL key-value data store used as a database, cache, and message broker. The database is stored in the server's RAM to enable fast access.

    sudo apt install redis-tools        // install redis

    redis-cli -h {target_IP}            // specify the hostname fo the target to connect to

The ```info``` command (once on the server) provides information and statitics about the server. The ```keyspace``` section of this output provides information about the main dictionary of each database. Statistics include the number of keys and the number of keys with expirations. The ```select``` command along with the index number of the database we want will let us select which database. We can also list all keys in the database using ```keys *```. We can get the key we want using ```get {key_name}```.