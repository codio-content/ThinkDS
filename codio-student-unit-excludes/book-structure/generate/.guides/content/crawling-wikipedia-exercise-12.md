Now it's time to write the crawler.  In the repository for this book, you'll find the source files for this exercise:



*  `WikiCrawler.java`, which contains starter code for your
crawler.

*  `WikiCrawlerTest.java`, which contains test code for
`WikiCrawler`.

*  `JedisIndex.java`, which is my solution to the previous
exercise.



You'll also need some of the helper classes we've used in previous exercises:



*   `JedisMaker.java`
*   `WikiFetcher.java`
*   `TermCounter.java`
*   `WikiNodeIterable.java`


Before you run `JedisMaker`, you have to provide a file with information about your Redis server. If you did this in the previous exercise, you should be all set. Otherwise you can find instructions in Section 14.3.


Run `ant build` to compile the source files, then run `ant JedisMaker` to make sure it is configured to connect to your Redis server.

Now run `ant WikiCrawlerTest`. It should fail, because you have work to do!

Here's the beginning of the `WikiCrawler` class I provided:

```code
public class WikiCrawler {

    public final String source;
    private JedisIndex index;
    private Queue<String> queue = new LinkedList<String>();
    final static WikiFetcher wf = new WikiFetcher();

    public WikiCrawler(String source, JedisIndex index) {
        this.source = source;
        this.index = index;
        queue.offer(source);
    }

    public int queueSize() {
        return queue.size();
    }
}
```

The instance variables are



* 
`source` is the URL where we start crawling.

* 
`index` is the `JedisIndex` where the results should go.

* 
`queue` is a `LinkedList` where we keep track of URLs
that have been discovered but not yet indexed.

* 
`wf` is the `WikiFetcher` we'll use to read and parse
Web pages.


Your job is to fill in `crawl`. Here's the prototype:


```code
    public String crawl(boolean testing) throws IOException {}
```

The parameter `testing` will be `true` when this method is called from `WikiCrawlerTest` and should be `false` otherwise.

When `testing` is `true`, the `crawl` method should:



* 
Choose and remove a URL from the queue in FIFO order.

* 
Read the contents of the page using
`WikiFetcher.readWikipedia`, which reads cached copies of pages
included in the repository for testing purposes (to avoid
problems if the Wikipedia version changes).

* 
It should index pages regardless of whether they are already indexed.

* 
It should find all the internal links on the page and add them to the
queue in the order they appear. “Internal links” are links to other
Wikipedia pages.

* 
And it should return the URL of the page it indexed.


When `testing` is `false`, this method should:



* 
Choose and remove a URL from the queue in FIFO order.

* 
If the URL is already indexed, it should not index it again, and
should return `null`.

* 
Otherwise it should read the contents of the page using
`WikiFetcher.fetchWikipedia`, which reads current content from
the Web.

* 
Then it should index the page, add links to the queue, and return the
URL of the page it indexed.


`WikiCrawlerTest` loads the queue with about 200 links and then invokes `crawl` three times. After each invocation, it checks the return value and the new length of the queue.

When your crawler is working as specified, this test should pass. Good luck!