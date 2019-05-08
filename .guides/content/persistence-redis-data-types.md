Redis is basically a map from keys, which are strings, to values, which can be one of several data types. The most basic Redis data type is a \redis{string}.  I will write Redis types in italics to distinguish them from Java types. 

To add a \redis{string} to the database, use `jedis.set`, which is similar to `Map.put`; the parameters are the new key and the corresponding value. To look up a key and get its value, use `jedis.get`:

```code
        jedis.set("mykey", "myvalue");
        String value = jedis.get("mykey");
```

In this example, the key is `"mykey"` and the value is `"myvalue"`.


Redis provides a \redis{set} structure, which is similar to a Java `Set<String>`. To add elements to a Redis \redis{set}, you choose a key to identify the \redis{set} and then use `jedis.sadd`:

```code
        jedis.sadd("myset", "element1", "element2", "element3");
        boolean flag = jedis.sismember("myset", "element2");
```

You don't have to create the \redis{set} as a separate step. If it doesn't exist, Redis creates it. In this case, it creates a \redis{set} named `myset` that contains three elements.

The method `jedis.sismember` checks whether an element is in a \redis{set}. Adding elements and checking membership are constant time operations.


Redis also provides a \redis{list} structure, which is similar to a Java `List<String>`. The method `jedis.rpush` adds elements to the end (right side) of a \redis{list}:

```code
        jedis.rpush("mylist", "element1", "element2", "element3");
        String element = jedis.lindex("mylist", 1);
```

Again, you don't have to create the structure before you start adding elements. This example creates a \redis{list} named “mylist” that contains three elements.


The method `jedis.lindex` takes an integer index and returns the indicated element of a \redis{list}. Adding and accessing elements are constant time operations.

Finally, Redis provides a \redis{hash} structure, which is similar to a Java `Map<String, String>`. The method `jedis.hset` adds a new entry to the \redis{hash}:

```code
        jedis.hset("myhash", "word1", Integer.toString(2));
        String value = jedis.hget("myhash", "word1");
```

This example creates a \redis{hash} named `myhash` that contains one entry, which maps from the key `word1` to the value `"2"`.

The keys and values are \redis{string}s, so if we want to store an `Integer`, we have to convert it to a `String` before we call `hset`.  And when we look up the value using `hget`, the result is a `String`, so we might have to convert it back to `Integer`.


Working with Redis \redis{hash}es can be confusing, because we use a key to identify which \redis{hash} we want, and then another key to identify a value in the \redis{hash}. In the context of Redis, the second key is called a “field”, which might help keep things straight. So a “key” like `myhash` identifies a particular \redis{hash}, and then a “field” like `word1` identifies a value in the \redis{hash}.

For many applications, the values in a Redis \redis{hash} are integers, so Redis provides a few special methods, like `hincrby`, that treat the values as numbers:

```code
        jedis.hincrBy("myhash", "word2", 1);
```

This method accesses `myhash`, gets the current value associated with `word2` (or 0 if it doesn't already exist), increments it by 1, and writes the result back to the \redis{hash}.

Setting, getting, and incrementing entries in a \redis{hash} are constant time operations.


You can read more about Redis data types at [http://thinkdast.com/redistypes](http://thinkdast.com/redistypes).