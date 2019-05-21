In this section I present a solution to the previous exercise and analyze the performance of the core methods.  Here are `findEntry` and `equals`:

```code
private Entry findEntry(Object target) {
    for (Entry entry: entries) {
        if (equals(target, entry.getKey())) {
            return entry;
        }
    }
    return null;
}

private boolean equals(Object target, Object obj) {
    if (target == null) {
        return obj == null;
    }
    return target.equals(obj);
}
```

The runtime of `equals` might depend on the size of the `target` and the keys, but does not generally depend on the number of entries, $n$. So `equals` is constant time.


In `findEntry`, we might get lucky and find the key we're looking for at the beginning, but we can't count on it. In general, the number of entries we have to search is proportional to $n$, so `findEntry` is linear.


Most of the core methods in `MyLinearMap` use `findEntry`, including `put`, `get`, and `remove`. Here's what they look like:

```code
public V put(K key, V value) {
    Entry entry = findEntry(key);
    if (entry == null) {
        entries.add(new Entry(key, value));
        return null;
    } else {
        V oldValue = entry.getValue();
        entry.setValue(value);
        return oldValue;
    }
}
```

```code
public V get(Object key) {
    Entry entry = findEntry(key);
    if (entry == null) {
        return null;
    }
    return entry.getValue();
}
```
    
```code
public V remove(Object key) {
    Entry entry = findEntry(key);
    if (entry == null) {
        return null;
    } else {
        V value = entry.getValue();
        entries.remove(entry);
        return value;
    }
}
```

After `put` calls `findEntry`, everything else is constant time. Remember that `entries` is an `ArrayList`, so adding an element *at the end* is constant time, on average. If the key is already in the map, we don't have to add an entry, but we have to call `entry.getValue` and `entry.setValue`, and those are both constant time. Putting it all together, `put` is linear.


By the same reasoning, `get` is also linear.

`remove` is slightly more complicated because `entries.remove` might have to remove an element from the beginning or middle of the `ArrayList`, and that takes linear time. But that's OK: two linear operations are still linear.


In summary, the core methods are all linear, which is why we called this implementation `MyLinearMap` (ta-da!).

If we know that the number of entries will be small, this implementation might be good enough, but we can do better. In fact, there is an implementation of `Map` where all of the core methods are constant time. When you first hear that, it might not seem possible. What we are saying, in effect, is that you can find a needle in a haystack in constant time, regardless of how big the haystack is. It's magic.


I'll explain how it works in two steps:



1.  Instead of storing entries in one big `List`, we'll break them up into lots of short lists. For each key, we'll use a **hash code** (explained in the next section) to determine which list to use.
1.  Using lots of short lists is faster than using just one, but as I'll explain, it doesn't change the order of growth; the core operations are still linear. But there is one more trick: if we increase the number of lists to limit the number of entries per list, the result is a constant-time map. You'll see the details in the next exercise, but first: hashing! 



In the next chapter, I'll present a solution, analyze the performance of the core `Map` methods, and introduce a more efficient implementation.