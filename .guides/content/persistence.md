In the next few exercises we will get back to building a web search engine. To review, the components of a search engine are:



* 
Crawling: We'll need a program that can download a web page, parse it,
and extract the text and any links to other pages.

* 
Indexing: We'll need an index that makes it possible to look up a
search term and find the pages that contain it.

* 
Retrieval: And we'll need a way to collect results from the index and
identify pages that are most relevant to the search terms.



If you did Exercise 8.3, you implemented an index using Java maps. In this exercise, we'll revisit the indexer and make a new version that stores the results in a database.


If you did Exercise 7.4, you built a crawler that follows the first link it finds. In the next exercise, we'll make a more general version that stores every link it finds in a queue and explores them in order.

And then, finally, you will work on the retrieval problem.

In these exercises, I provide less starter code, and you will make more design decisions. These exercises are also more open-ended. I will suggest some minimal goals you should try to reach, but there are many ways you can go farther if you want to challenge yourself.

Now, let's get started on a new version of the indexer.