If you did the “Getting to Philosophy” exercise in Chapter 7, you already have a program that reads a Wikipedia page, finds the first link, uses the link to load the next page, and repeats. This program is a specialized kind of crawler, but when people say “Web crawler” they usually mean a program that



*  Loads a starting page and indexes the contents,
*  Finds all the links on the page and adds the linked URLs to a collection, and
*  Works its way through the collection, loading pages, indexing them, and adding new URLs.
*  If it finds a URL that has already been indexed, it skips it. 

You can think of the Web as a graph where each page is a node and each link is a directed edge from one node to another. If you are not familiar with graphs, you can read about them at [http://thinkdast.com/graph](http://thinkdast.com/graph).


Starting from a source node, a crawler traverses this graph, visiting each reachable node once.


The collection we use to store the URLs determines what kind of traversal the crawler performs:



*  If it's a first-in-first-out (FIFO) queue, the crawler performs a breadth-first traversal.
*  If it's a last-in-first-out (LIFO) stack, the crawler performs a depth-first traversal.
*  More generally, the items in the collection might be prioritized. For example, we might want to give higher priority to pages that have not been indexed for a long time. 

You can read more about graph traversal at [http://thinkdast.com/graphtrav](http://thinkdast.com/graphtrav).