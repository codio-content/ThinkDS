We've shown that `containsKey`, `get`, and `remove` are constant time, and `put` is constant time on average. We should take a minute to appreciate how remarkable that is. The performance of these operations is pretty much the same no matter how big the hash table is. Well, sort of.


Remember that our analysis is based on a simple model of computation where each “unit of work” takes the same amount of time. Real computers are more complicated than that. In particular, they are usually fastest when working with data structures small enough to fit in cache; somewhat slower if the structure doesn't fit in cache but still fits in memory; and *much* slower if the structure doesn't fit in memory.


Another limitation of this implementation is that hashing doesn't help if we are given a value rather than a key: `containsValue` is linear because it has to search all of the sub-maps. And there is no particularly efficient way to look up a value and find the corresponding key (or possibly keys).


And there's one more limitation: some of the methods that were constant time in `MyLinearMap` have become linear. For example:

```code
    public void clear() {
        for (int i=0; i<maps.size(); i++) {
            maps.get(i).clear();
        }
    }
```

`clear` has to clear all of the sub-maps, and the number of sub-maps is proportional to $n$, so it's linear. Fortunately, this operation is not used very often, so for most applications this tradeoff is acceptable.