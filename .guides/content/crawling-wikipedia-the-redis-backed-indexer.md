In my solution, we store two kinds of structures in Redis:



*  For each search term, we have a `URLSet`, which is a Redis \redis{set} of URLs that contain the search term.
*  For each URL, we have a `TermCounter`, which is a Redis \redis{hash} that maps each search term to the number of times it appears. 

We discussed these data types in the previous chapter. You can also read about Redis structures at [http://thinkdast.com/redistypes](http://thinkdast.com/redistypes)


In `JedisIndex`, I provide a method that takes a search term and returns the Redis key of its `URLSet`:

```code
private String urlSetKey(String term) {
    return "URLSet:" + term;
}
```

And a method that takes a URL and returns the Redis key of its `TermCounter`:

```code
private String termCounterKey(String url) {
    return "TermCounter:" + url;
}
```

Here's the implementation of `indexPage`, which takes a URL and a jsoup `Elements` object that contains the DOM tree of the paragraphs we want to index:

```code
public void indexPage(String url, Elements paragraphs) {
    System.out.println("Indexing " + url);

    // make a TermCounter and count the terms in the paragraphs
    TermCounter tc = new TermCounter(url);
    tc.processElements(paragraphs);

    // push the contents of the TermCounter to Redis
    pushTermCounterToRedis(tc);
}
```

To index a page, we



1.  Make a Java `TermCounter` for the contents of the page, using code from a previous exercise.
1.  Push the contents of the `TermCounter` to Redis. 

Here's the new code that pushes a `TermCounter` to Redis:

```code
public List<Object> pushTermCounterToRedis(TermCounter tc) {
    Transaction t = jedis.multi();

    String url = tc.getLabel();
    String hashname = termCounterKey(url);

    // if this page has already been indexed, delete the old hash
    t.del(hashname);

    // for each term, add an entry in the TermCounter and a new
    // member of the index
    for (String term: tc.keySet()) {
        Integer count = tc.get(term);
        t.hset(hashname, term, count.toString());
        t.sadd(urlSetKey(term), url);
    }
    List<Object> res = t.exec();
    return res;
}
```

This method uses a `Transaction` to collect the operations and send them to the server all at once, which is much faster than sending a series of small operations.


It loops through the terms in the `TermCounter`. For each one it



1.  Finds or creates a `TermCounter` on Redis, then adds a field for the new term.
1.  Finds or creates a `URLSet` on Redis, then adds the current URL. 

If the page has already been indexed, we delete its old `TermCounter` before pushing the new contents.

That's it for indexing new pages.


The second part of the exercise asked you to write `getCounts`, which takes a search term and returns a map from each URL where the term appears to the number of times it appears there. Here is my solution:

```code
    public Map<String, Integer> getCounts(String term) {
        Map<String, Integer> map = new HashMap<String, Integer>();
        Set<String> urls = getURLs(term);
        for (String url: urls) {
            Integer count = getCount(url, term);
            map.put(url, count);
        }
        return map;
    }
```

This method uses two helper methods:



*  `getURLs` takes a search term and returns the Set of URLs where the term appears.
*  `getCount` takes a URL and a term and returns the number of times the term appears at the given URL. 

Here are the implementations:

```code
    public Set<String> getURLs(String term) {
        Set<String> set = jedis.smembers(urlSetKey(term));
        return set;
    }

    public Integer getCount(String url, String term) {
        String redisKey = termCounterKey(url);
        String count = jedis.hget(redisKey, term);
        return new Integer(count);
    }
```

Because of the way we designed the index, these methods are simple and efficient.