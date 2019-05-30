In the repository for this book, you'll find some code to help you get started:



1.  `WikiNodeExample.java` contains the code from the previous chapter, demonstrating recursive and iterative implementations of depth-first search (DFS) in a DOM tree.
1.  `WikiNodeIterable.java` contains an `Iterable` class for traversing a DOM tree. I'll explain this code in the next section.
1.  `WikiFetcher.java` contains a utility class that uses jsoup to download pages from Wikipedia. To help you comply with Wikipedia's terms of service, this class limits how fast you can download pages; if you request more than one page per second, it sleeps before downloading the next page.
1.  `WikiPhilosophy.java` contains an outline of the code you will write for this exercise. We'll walk through it below. 

{Run Wiki Fetcher | terminal}(cd code && javac WikiFetcher.java && java -cp lib/*:. WikiFetcher && cd ../)
