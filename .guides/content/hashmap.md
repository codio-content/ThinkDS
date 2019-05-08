In the previous chapter, we wrote an implementation of the `Map` interface that uses hashing.  We expect this version to be faster, because the lists it searches are shorter, but the order of growth is still linear.


If there are $n$ entries and $k$ sub-maps, the size of the sub-maps is $n/k$ on average, which is still proportional to $n$.  But if we increase $k$ along with $n$, we can limit the size of $n/k$.

For example, suppose we double $k$ every time $n$ exceeds $k$; in that case the number of entries per map would be less than 1 on average, and pretty much always less than 10, as long as the hash function spreads out the keys reasonably well.


If the number of entries per sub-map is constant, we can search a single sub-map in constant time. And computing the hash function is generally constant time (it might depend on the size of the key, but does not depend on the number of keys). That makes the core `Map` methods, `put` and `get`, constant time.

In the next exercise, you'll see the details.