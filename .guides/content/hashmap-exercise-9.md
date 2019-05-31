In `MyHashMap.java`, I provide the outline of a hash table that grows when needed. Here's the beginning of the definition: [Highlight in Code](open_file code/MyHashMap.java panel=0 ref="public class MyHashMap" count=15)



`MyHashMap` extends `MyBetterMap`, so it inherits the methods defined there. The only method it overrides is `put` which calls `put` in the superclass --- that is, it calls the version of `put` in `MyBetterMap` --- and then it checks whether it has to rehash. Calling `size` returns the total number of entries, $n$. Calling `maps.size` returns the number of embedded maps, $k$.


The constant `FACTOR`, which is called the **load factor**, determines the maximum number of entries per sub-map, on average. If `n > k * FACTOR`, that means `n/k > FACTOR`, which means the number of entries per sub-map exceeds the threshold, so we call `rehash`.


{Check It!|assessment}(test-2138140034)

It should fail because the implementation of `rehash` throws an exception. Your job is to fill it in.




Fill in the body of `rehash` to collect the entries in the table, resize the table, and then put the entries back in. I provide two methods that might come in handy: `MyBetterMap.makeMaps` and `MyLinearMap.getEntries`. Your solution should double the number of maps, $k$, each time it is called.