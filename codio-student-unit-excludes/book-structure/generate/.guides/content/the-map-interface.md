In the next few exercises, I present several implementations of the `Map` interface. One of them is based on a **hash table**, which is arguably the most magical data structure ever invented. Another, which is similar to `TreeMap`, is not quite as magical, but it has the added capability that it can iterate the elements in order.


You will have a chance to implement these data structures, and then we will analyze their performance.

But before we can explain hash tables, we'll start with a simple implementation of a `Map` using a `List` of key-value pairs.