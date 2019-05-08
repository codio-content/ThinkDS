A **web search engine**, like Google Search or Bing, takes a set of “search terms” and returns a list of web pages that are relevant to those terms (I'll discuss what “relevant” means later).  You can read more at [http://thinkdast.com/searcheng](http://thinkdast.com/searcheng), but I'll explain what you need as we go along.


The essential components of a search engine are:



* 
Crawling: We'll need a program that can download a web page, parse it,
and extract the text and any links to other pages.

* 
Indexing: We'll need a data structure that makes it possible to look up a
search term and find the pages that contain it.

* 
Retrieval: And we'll need a way to collect results from the Index and
identify pages that are most relevant to the search terms.


We'll start with the crawler.  The goal of a crawler is to discover and download a set of web pages. For search engines like Google and Bing, the goal is to find *all* web pages, but often crawlers are limited to a smaller domain. In our case, we will only read pages from Wikipedia.


As a first step, we'll build a crawler that reads a Wikipedia page, finds the first link, follows the link to another page, and repeats. We will use this crawler to test the “Getting to Philosophy” conjecture, which states:



> Clicking on the first lowercase link in the main text of a
> Wikipedia article, and then repeating the process for subsequent
> articles, usually eventually gets one to the Philosophy article.


This conjecture is stated at [http://thinkdast.com/getphil](http://thinkdast.com/getphil){}, and you can read its history there.

Testing the conjecture will allow us to build the basic pieces of a crawler without having to crawl the entire web, or even all of Wikipedia. And I think the exercise is kind of fun!

In a few chapters, we'll work on the indexer, and then we'll get to the retriever.