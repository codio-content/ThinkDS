Using the data structures we designed, how long will it take to index a page? Again, think about your answer before you continue.


To index a page, we traverse its DOM tree, find all the `TextNode` objects, and split up the strings into search terms. That all takes time proportional to the number of words on the page.


For each term, we increment a counter in a HashMap, which is a constant time operation. So making the `TermCounter` takes time proportional to the number of words on the page.


Pushing the `TermCounter` to Redis requires deleting a `TermCounter`, which is linear in the number of unique terms. Then for each term we have to



1. 
Add an element to a `URLSet`, and

1. 
Add an element to a Redis `TermCounter`.


Both of these are constant time operations, so the total time to push the `TermCounter` is linear in the number of unique search terms.


In summary, making the `TermCounter` is proportional to the number of words on the page. Pushing the `TermCounter` to Redis is proportional to the number of unique terms.


Since the number of words on the page usually exceeds the number of unique search terms, the overall complexity is proportional to the number of words on the page. In theory a page might contain all search terms in the index, so the worst case performance is $O(M)$, but we don't expect to see the worse case in practice.

This analysis suggests a way to improve performance: we should probably avoid indexing very common words. First of all, they take up a lot of time and space, because they appear in almost every `URLSet` and `TermCounter`. Furthermore, they are not very useful because they don't help identify relevant pages.


Most search engines avoid indexing common words, which are known in this context as stop words ([http://thinkdast.com/stopword](http://thinkdast.com/stopword)).