At this point you should be familiar with the `Map` interface and the `HashMap` implementation provided by Java. And by making your own `Map` using a hash table, you should understand how `HashMap` works and why we expect its core methods to be constant time.


Because of this performance, `HashMap` is widely used, but it is not the only implementation of `Map`. There are a few reasons you might want another implementation:



1. 
Hashing can be slow, so even though `HashMap` operations are
constant time, the “constant” might be big.

1. 
Hashing works well if the hash function distributes the keys evenly
among the sub-maps.  But designing good hash functions is not easy,
and if too many keys end up in the same sub-map, the performance of
the `HashMap` may be poor.

1. 
The keys in a hash table are not stored in any particular order; in
fact, the order might change when the table grows and the keys are
rehashed. For some applications, it is necessary, or at least useful,
to keep the keys in order.


It is hard to solve all of these problems at the same time, but Java provides an implementation called `TreeMap` that comes close:



1. 
It doesn't use a hash function, so it avoids the cost of hashing
and the difficulty of choosing a hash function.

1. 
Inside the `TreeMap`, the keys are are stored in a
**binary search tree**, which makes it possible to traverse the
keys, in order, in linear time.

1. 
The runtime of the core methods is proportional to $\log n$,
which is not quite as good as constant time, but it is still
very good.


In the next section, I'll explain how binary search trees work and then you will use one to implement a `Map`. Along the way, we'll analyze the performance of the core map methods when implemented using a tree.