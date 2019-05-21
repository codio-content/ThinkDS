In the repository for this book you'll find the source files for this exercise:



*  `WikiSearch.java`, which defines an object that contains search results and performs operations on them.
*  `WikiSearchTest.java`, which contains test code for `WikiSearch`.
*  `Card.java`, which demonstrates how to use the `sort` method in `java.util.Collections`. 

You will also find some of the helper classes we've used in previous exercises.


Here's the beginning of the `WikiSearch` class definition:

```code
public class WikiSearch {

    // map from URLs that contain the term(s) to relevance score
    private Map<String, Integer> map;

    public WikiSearch(Map<String, Integer> map) {
        this.map = map;
    }

    public Integer getRelevance(String url) {
        Integer relevance = map.get(url);
        return relevance==null ? 0: relevance;
    }
}
```

A `WikiSearch` object contains a map from URLs to their relevance score. In the context of information retrieval, a “relevance score” is a number intended to indicate how well a page meets the needs of the user as inferred from the query. There are many ways to construct a relevance score, but most of them are based on “term frequency”, which is the number of times the search terms appear on the page. A common relevance score is called TF-IDF, which stands for “term frequency -- inverse document frequency”.  You can read more about it at [http://thinkdast.com/tfidf](http://thinkdast.com/tfidf).


You'll have the option to implement TF-IDF later, but we'll start with something even simpler, TF:



*  If a query contains a single search term, the relevance of a page is its term frequency; that is, the number of time the term appears on the page.
*  For queries with multiple terms, the relevance of a page is the sum of the term frequencies; that is, the total number of times any of the search terms appear. 

Now you're ready to start the exercise. Run `ant build` to compile the source files, then run `ant WikiSearchTest`. As usual, it should fail, because you have work to do.


In `WikiSearch.java`, fill in the bodies of `and`, `or`, and `minus` so that the relevant tests pass. You don't have to worry about `testSort` yet.


You can run `WikiSearchTest` without using Jedis because it doesn't depend on the index in your Redis database. But if you want to run a query against your index, you have to provide a file with information about your Redis server.  See Section 14.3 for details.


Run `ant JedisMaker` to make sure it is configured to connect to your Redis server. Then run `WikiSearch`, which prints results from three queries:



*  “java”
*  “programming”
*  “java AND programming” 

Initially the results will be in no particular order, because `WikiSearch.sort` is incomplete.


Fill in the body of `sort` so the results are returned in increasing order of relevance. I suggest you use the `sort` method provided by `java.util.Collections`, which sorts any kind of `List`. You can read the documentation at [http://thinkdast.com/collections](http://thinkdast.com/collections).

There are two versions of `sort`:



*  The one-parameter version takes a list and sorts the elements using the `compareTo` method, so the elements have to be `Comparable`.
*  The two-parameter version takes a list of any object type and a `Comparator`, which is an object that provides a `compare` method that compares elements. 


If you are not familiar with the `Comparable` and `Comparator` interfaces, I explain them in the next section.