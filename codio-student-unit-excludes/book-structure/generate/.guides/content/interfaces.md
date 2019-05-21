This book presents three topics:



*  Data structures: Starting with the structures in the Java Collections Framework (JCF), you will learn how to use data structures like lists and maps, and you will see how they work.
*  Analysis of algorithms: I present techniques for analyzing code and predicting how fast it will run and how much space (memory) it will require.
*  Information retrieval: To motivate the first two topics, and to make the exercises more interesting, we will use data structures and algorithms to build a simple web search engine. 

Here's an outline of the order of topics:



*  We'll start with the `List` interface and you will write classes that implement this interface two different ways.  Then we'll compare your implementations with the Java classes `ArrayList` and `LinkedList`.
*  Next I'll introduce tree-shaped data structures and you will work on the first application: a program that reads pages from Wikipedia, parses the contents, and navigates the resulting tree to find links and other features.  We'll use these tools to test the “Getting to Philosophy” conjecture (you can get a preview by reading [http://thinkdast.com/getphil](http://thinkdast.com/getphil)).
*  We'll learn about the `Map` interface and Java's `HashMap` implementation.  Then you'll write classes that implement this interface using a hash table and a binary search tree.
*  Finally, you will use these classes (and a few others I'll present along the way) to implement a web search engine, including: a crawler that finds and reads pages, an indexer that stores the contents of Web pages in a form that can be searched efficiently, and a retriever that takes queries from a user and returns relevant results. 

Let's get started.