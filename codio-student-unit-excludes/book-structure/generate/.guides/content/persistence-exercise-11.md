At this point you have the information you need to make a web search index that stores results in a Redis database.


Now run `ant JedisIndexTest`. It should fail, because you have some work to do!

`JedisIndexTest` tests these methods:



*  `JedisIndex`, which is the constructor that takes a `Jedis` object as a parameter.
*  `indexPage`, which adds a Web page to the index; it takes a `String` URL and a jsoup `Elements` object that contains the elements of the page that should be indexed.
*  `getCounts`, which takes a search term and returns a `Map<String, Integer>` that maps from each URL that contains the search term to the number of times it appears on that page. 

Here's an example of how these methods are used:

```code
        WikiFetcher wf = new WikiFetcher();
        String url1 = 
            "http://en.wikipedia.org/wiki/Java_(programming_language)";
        Elements paragraphs = wf.readWikipedia(url1);

        Jedis jedis = JedisMaker.make();
        JedisIndex index = new JedisIndex(jedis);
        index.indexPage(url1, paragraphs);
        Map<String, Integer> map = index.getCounts("the");
```

If we look up `url1` in the result, `map`, we should get 339, which is the number of times the word “the” appears on the Java Wikipedia page (that is, the version we saved).


If we index the same page again, the new results should replace the old ones.

One suggestion for translating data structures from Java to Redis: remember that each object in a Redis database is identified by a unique key, which is a `string`. If you have two kinds of objects in the same database, you might want to add a prefix to the keys to distinguish between them. For example, in our solution, we have two kinds of objects:



*  We define a `URLSet` to be a Redis `set` that contains the URLs that contain a given search term. The key for each `URLSet` starts with `"URLSet:"`, so to get the URLs that contain the word “the”, we access the `set` with the key `"URLSet:the"`.
*  We define a `TermCounter` to be a Redis `hash` that maps from each term that appears on a page to the number of times it appears. The key for each `TermCounter` starts with `"TermCounter:"` and ends with the URL of the page we're looking up. 


In my implementation,  there is one `URLSet` for each term and one `TermCounter` for each indexed page. I provide two helper methods, `urlSetKey` and `termCounterKey`, to assemble these keys.