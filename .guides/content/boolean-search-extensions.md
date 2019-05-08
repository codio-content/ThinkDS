If you get a basic version of this exercise working, you might want to work on these optional exercises:



*  Read about TF-IDF at [http://thinkdast.com/tfidf](http://thinkdast.com/tfidf)
and implement it. You might have to modify `JavaIndex` to
compute document frequencies; that is, the total number of times
each term appears on all pages in the index.

*  For queries with more than one search term, the total relevance for
each page is currently the sum of the relevance for each term. Think
about when this simple version might not work well, and try out some
alternatives.

*  Build a user interface that allows users to enter queries with
boolean operators. Parse the queries, generate the results, then
sort them by relevance and display the highest-scoring
URLs. Consider generating “snippets” that show where the search
terms appeared on the page. If you want to make a Web application
for your user interface, consider using Heroku as a simple option
for developing and deploying Web applications using Java.  See
[http://thinkdast.com/heroku](http://thinkdast.com/heroku).