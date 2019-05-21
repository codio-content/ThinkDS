`TermCounter` is a class that represents a mapping from search terms to the number of times they appear in a page. Here is the first part of the class definition:

```code
public class TermCounter {

    private Map<String, Integer> map;
    private String label;

    public TermCounter(String label) {
        this.label = label;
        this.map = new HashMap<String, Integer>();
    }
}
```

The instance variables are `map`, which contains the mapping from terms to counts, and `label`, which identifies the document the terms came from; we'll use it to store URLs.


To implement the mapping, I chose `HashMap`, which is the most commonly-used `Map`. Coming up in a few chapters, you will see how it works and why it is a common choice.

`TermCounter` provides `put` and `get`, which are defined like this:

```code
    public void put(String term, int count) {
        map.put(term, count);
    }

    public Integer get(String term) {
        Integer count = map.get(term);
        return count == null ? 0 : count;
    }
```

`put` is just a **wrapper method**; when you call `put` on a `TermCounter`, it calls `put` on the embedded map.


On the other hand, `get` actually does some work. When you call `get` on a `TermCounter`, it calls `get` on the map, and then checks the result. If the term does not appear in the map, `TermCount.get` returns 0. Defining `get` this way makes it easier to write `incrementTermCount`, which takes a term and increases by one the counter associated with that term.

```code
    public void incrementTermCount(String term) {
        put(term, get(term) + 1);
    }
```

If the term has not been seen before, `get` returns 0; we add 1, then use `put` to add a new key-value pair to the map. If the term is already in the map, we get the old count, add 1, and then store the new count, which replaces the old value.

In addition, `TermCounter` provides these other methods to help with indexing Web pages:

```code
    public void processElements(Elements paragraphs) {
        for (Node node: paragraphs) {
            processTree(node);
        }
    }

    public void processTree(Node root) {
        for (Node node: new WikiNodeIterable(root)) {
            if (node instanceof TextNode) {
                processText(((TextNode) node).text());
            }
        }
    }

    public void processText(String text) {
        String[] array = text.replaceAll("\\pP", " ").
                              toLowerCase().
                              split("\\s+");

        for (int i=0; i<array.length; i++) {
            String term = array[i];
            incrementTermCount(term);
        }
    }
```



*  `processElements` takes an `Elements` object, which is a collection of jsoup `Element` objects. It iterates through the collection and calls `processTree` on each.
*  `processTree` takes a jsoup `Node` that represents the root of a DOM tree. It iterates through the tree to find the nodes that contain text; then it extracts the text and passes it to `processText`.
*  `processText` takes a `String` that contains words, spaces, punctuation, etc. It removes punctuation characters by replacing them with spaces, converts the remaining letters to lowercase, then splits the text into words. Then it loops through the words it found and calls `incrementTermCount` on each.  The `replaceAll` and `split` methods take **regular expressions** as parameters; you can read more about them at [http://thinkdast.com/regex](http://thinkdast.com/regex). 


Finally, here's an example that demonstrates how `TermCounter` is used:

```code
    String url = "http://en.wikipedia.org/wiki/Java_(programming_language)";
    WikiFetcher wf = new WikiFetcher();
    Elements paragraphs = wf.fetchWikipedia(url);

    TermCounter counter = new TermCounter(url);
    counter.processElements(paragraphs);
    counter.printCounts();
```

This example uses a `WikiFetcher` to download a page from Wikipedia and parse the main text. Then it creates a `TermCounter` and uses it to count the words in the page.


In the next section, you'll have a chance to run this code and test your understanding by filling in a missing method.