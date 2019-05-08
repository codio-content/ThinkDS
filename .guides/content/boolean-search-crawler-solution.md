First, let's go over our solution to the previous exercise. I provided an outline of `WikiCrawler`; your job was to fill in `crawl`. As a reminder, here are the fields in the `WikiCrawler` class:


```code
public class WikiCrawler {
    // keeps track of where we started
    private final String source;

    // the index where the results go
    private JedisIndex index;

    // queue of URLs to be indexed
    private Queue<String> queue = new LinkedList<String>();

    // fetcher used to get pages from Wikipedia
    final static WikiFetcher wf = new WikiFetcher();
}
```

When we create a `WikiCrawler`, we provide `source` and `index`. Initially, `queue` contains only one element, `source`.


Notice that the implementation of `queue` is a `LinkedList`, so we can add elements at the end --- and remove them from the beginning --- in constant time. By assigning a `LinkedList` object to a `Queue` variable, we limit ourselves to using methods in the `Queue` interface; specifically, we'll use `offer` to add elements and `poll` to remove them.


Here's my implementation of `WikiCrawler.crawl`:

```code
    public String crawl(boolean testing) throws IOException {
        if (queue.isEmpty()) {
            return null;
        }
        String url = queue.poll();
        System.out.println("Crawling " + url);

        if (testing==false && index.isIndexed(url)) {
            System.out.println("Already indexed.");
            return null;
        }

        Elements paragraphs;
        if (testing) {
            paragraphs = wf.readWikipedia(url);
        } else {
            paragraphs = wf.fetchWikipedia(url);
        }
        index.indexPage(url, paragraphs);
        queueInternalLinks(paragraphs);
        return url;
    }
```

Most of the complexity in this method is there to make it easier to test. Here's the logic:



* 
If the queue is empty, it returns `null` to indicate that it
did not index a page.

* 
Otherwise it removes and stores the next URL from the queue.

* 
If the URL has already been indexed, `crawl` doesn't index it
again, unless it's in testing mode.

* 
Next it reads the contents of the page: if it's in testing mode, it
reads from a file; otherwise it reads from the Web.

* 
It indexes the page.

* 
It parses the page and adds internal links to the queue.

* 
Finally, it returns the URL of the page it indexed.


I presented an implementation of `Index.indexPage` in Section 15.1. So the only new method is `WikiCrawler.queueInternalLinks`.


I wrote two versions of this method with different parameters: one takes an `Elements` object containing one DOM tree per paragraph; the other takes an `Element` object that contains a single paragraph.


The first version just loops through the paragraphs. The second version does the real work.

```code
    void queueInternalLinks(Elements paragraphs) {
        for (Element paragraph: paragraphs) {
            queueInternalLinks(paragraph);
        }
    }

    private void queueInternalLinks(Element paragraph) {
        Elements elts = paragraph.select("a[href]");
        for (Element elt: elts) {
            String relURL = elt.attr("href");

            if (relURL.startsWith("/wiki/")) {
                String absURL = elt.attr("abs:href");
                queue.offer(absURL);
            }
        }
    }
```


To determine whether a link is “internal,” we check whether the URL starts with “/wiki/”. This might include some pages we don't want to index, like meta-pages about Wikipedia. And it might exclude some pages we want, like links to pages in non-English languages. But this simple test is good enough to get started.


That's all there is to it. This exercise doesn't have a lot of new material; it is mostly a chance to bring the pieces together.