Suppose we have indexed $N$ pages and discovered $M$ unique search terms. How long will it take to look up a search term? Think about your answer before you continue.


To look up a search term, we run `getCounts`, which



1.  Creates a map.
1.  Runs `getURLs` to get a Set of URLs.
1.  For each URL in the Set, runs `getCount` and adds an entry to a `HashMap`. 

`getURLs` takes time proportional to the number of URLs that contain the search term. For rare terms, that might be a small number, but for common terms it might be as large as $N$.

Inside the loop, we run `getCount`, which finds a `TermCounter` on Redis, looks up a term, and adds an entry to a HashMap. Those are all constant time operations, so the overall complexity of `getCounts` is $O(N)$ in the worst case. However, in practice the runtime is proportional to the number of pages that contain the term, which is normally much less than $N$.


This algorithm is as efficient as it can be, in terms of algorithmic complexity, but it is very slow because it sends many small operations to Redis. You can make it faster using a `Transaction`. You might want to do that as an exercise, or you can see my solution in `RedisIndex.java`.