At this point you have all the information you need to do the exercise, so you can get started if you are ready. But I have a few suggestions you might want to read first:



*  For this exercise I provide less guidance than in previous exercises.  You will have to make some design decisions; in particular, you will have to figure out how to divide the problem into pieces that you can test one at a time, and then assemble the pieces into a complete solution. If you try to write the whole thing at once, without testing smaller pieces, it might take a very long time to debug.
*  One of the challenges of working with persistent data is that it is persistent. The structures stored in the database might change every time you run the program. If you mess something up in the database, you will have to fix it or start over before you can proceed. To help you keep things under control, I've provided methods called `deleteURLSets`, `deleteTermCounters`, and `deleteAllKeys`, which you can use to clean out the database and start fresh. You can also use `printIndex` to print the contents of the index.
*  Each time you invoke a `Jedis` method, your client sends a message to the server, then the server performs the action you requested and sends back a message. If you perform many small operations, it will probably take a long time. You can improve performance by grouping a series of operations into a `Transaction`. 

For example, here's a simple version of `deleteAllKeys`:

```code
    public void deleteAllKeys() {
        Set<String> keys = jedis.keys("*");
        for (String key: keys) {
            jedis.del(key);
        }
    }
```

Each time you invoke `del` requires a round-trip from the client to the server and back. If the index contains more than a few pages, this method would take a long time to run. We can speed it up with a `Transaction` object:


```code
    public void deleteAllKeys() {
        Set<String> keys = jedis.keys("*");
        Transaction t = jedis.multi();
        for (String key: keys) {
            t.del(key);
        }
        t.exec();
    }
```

`jedis.multi` returns a `Transaction` object, which provides all the methods of a `Jedis` object. But when you invoke a method on a `Transaction`, it doesn't run the operation immediately, and it doesn't communicate with the server. It saves up a batch of operations until you invoke `exec`. Then it sends all of the saved operations to the server at the same time, which is usually much faster.

{Run! | terminal}(cd code && javac JedisIndex.java JedisMaker.java WikiFetcher.java && java -cp lib/*:. JedisIndex && cd ../ )

{Check It!|assessment}(test-3509169483)
