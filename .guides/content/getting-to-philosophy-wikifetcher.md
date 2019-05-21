When you write a Web crawler, it is easy to download too many pages too fast, which might violate the terms of service for the server you are downloading from. To help you avoid that, I provide a class called `WikiFetcher` that does two things:



1.  It encapsulates the code we demonstrated in the previous chapter for downloading pages from Wikipedia, parsing the HTML, and selecting the content text.
1.  It measures the time between requests and, if we don't leave enough time between requests, it sleeps until a reasonable interval has elapsed. By default, the interval is one second. 

Here's the definition of `WikiFetcher`:

```code
public class WikiFetcher {
    private long lastRequestTime = -1;
    private long minInterval = 1000;

    /**
     * Fetches and parses a URL string, 
     * returning a list of paragraph elements.
     *
     * @param url
     * @return
     * @throws IOException
     */
    public Elements fetchWikipedia(String url) throws IOException {
        sleepIfNeeded();

        Connection conn = Jsoup.connect(url);
        Document doc = conn.get();
        Element content = doc.getElementById("mw-content-text");
        Elements paragraphs = content.select("p");
        return paragraphs;
    }

    private void sleepIfNeeded() {
        if (lastRequestTime != -1) {
            long currentTime = System.currentTimeMillis();
            long nextRequestTime = lastRequestTime + minInterval;
            if (currentTime < nextRequestTime) {
                try {
                    Thread.sleep(nextRequestTime - currentTime);
                } catch (InterruptedException e) {
                    System.err.println(
                        "Warning: sleep interrupted in fetchWikipedia.");
                }
            }
        }
        lastRequestTime = System.currentTimeMillis();
    }
}
```

The only public method is `fetchWikipedia`, which takes a URL as a `String` and returns an `Elements` collection that contains one DOM element for each paragraph in the content text. This code should look familiar.


The new code is in `sleepIfNeeded`, which checks the time since the last request and sleeps if the elapsed time is less than `minInterval`, which is in milliseconds.

That's all there is to `WikiFetcher`. Here's an example that demonstrates how it's used:

```code
    WikiFetcher wf = new WikiFetcher();

    for (String url: urlList) {
        Elements paragraphs = wf.fetchWikipedia(url);
        processParagraphs(paragraphs);
    }
```

In this example, we assume that `urlList` is a collection of `String`s, and `processParagraphs` is a method that does something with the `Elements` object returned by `fetchWikipedia`.

This example demonstrates something important: you should create one `WikiFetcher` object and use it to handle all requests. If you have multiple instances of `WikiFetcher`, they won't enforce the minimum interval between requests.


NOTE: My implementation of `WikiFetcher` is simple, but it would be easy for someone to misuse it by creating multiple instances. You could avoid this problem by making `WikiFetcher` a “singleton”, which you can read about at [http://thinkdast.com/singleton](http://thinkdast.com/singleton).