To improve the performance of `MyLinearMap`, we'll write a new class, called `MyBetterMap`, that contains a collection of `MyLinearMap` objects. It divides the keys among the embedded maps, so the number of entries in each map is smaller, which speeds up `findEntry` and the methods that depend on it.

Here's the beginning of the class definition: [Highlight in Code](open_file code/MyBetterMap.java panel=0 ref="public class MyBetterMap" count=23)



The instance variable, `maps`, is a collection of `MyLinearMap` objects. The constructor takes a parameter, `k`, that determines how many maps to use, at least initially. Then `makeMaps` creates the embedded maps and stores them in an `ArrayList`.


Now, the key to making this work is that we need some way to look at a key and decide which of the embedded maps it should go into. When we `put` a new key, we choose one of the maps; when we `get` the same key, we have to remember where we put it.


One possibility is to choose one of the sub-maps at random and keep track of where we put each key. But how should we keep track? It might seem like we could use a `Map` to look up the key and find the right sub-map, but the whole point of the exercise is to write an efficient implementation of a `Map`. We can't assume we already have one.

A better approach is to use a **hash function**, which takes an `Object`, any `Object`, and returns an integer called a **hash code**.  Importantly, if it sees the same `Object` more than once, it always returns the same hash code. That way, if we use the hash code to store a key, we'll get the same hash code when we look it up.


In Java, every `Object` provides a method called `hashCode` that computes a hash function. The implementation of this method is different for different objects; we'll see an example soon.


Here's a helper method that chooses the right sub-map for a given key: [Highlight in Code](open_file code/MyBetterMap.java panel=0 ref="protected MyLinearMap" count=4)



If `key` is `null`, we choose the sub-map with index 0, arbitrarily. Otherwise we use `hashCode` to get an integer, apply `Math.abs` to make sure it is non-negative, then use the remainder operator, `%`, which guarantees that the result is between 0 and `maps.size()-1`. So `index` is always a valid index into `maps`. Then `chooseMap` returns a reference to the map it chose.


We use `chooseMap` in both `put` and `get`, so when we look up a key, we get the same map we chose when we added the key. At least, we should --- I'll explain a little later why this might not work.

Here's my implementation of `put` and `get`:

```code
public V put(K key, V value) {
  MyLinearMap<K, V> map = chooseMap(key);
    return map.put(key, value);
}

public V get(Object key) {
    MyLinearMap<K, V> map = chooseMap(key);
    return map.get(key);
}
```

Pretty simple, right? In both methods, we use `chooseMap` to find the right sub-map and then invoke a method on the sub-map.  That's how it works; now let's think about performance.


If there are $n$ entries split up among $k$ sub-maps, there will be $n/k$ entries per map, on average. When we look up a key, we have to compute its hash code, which takes some time, then we search the corresponding sub-map.

Because the entry lists in `MyBetterMap` are $k$ times shorter than the entry list in `MyLinearMap`, we expect the search to be $k$ times faster. But the runtime is still proportional to $n$, so `MyBetterMap` is still linear. In the next exercise, you'll see how we can fix that.