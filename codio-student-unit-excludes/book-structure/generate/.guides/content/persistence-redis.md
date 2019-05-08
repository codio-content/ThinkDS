The previous version of the indexer stores the index in two data structures: a `TermCounter` that maps from a search term to the number of times it appears on a web page, and an `Index` that maps from a search term to the set of pages where it appears.

These data structures are stored in the memory of a running Java program, which means that when the program stops running, the index is lost. Data stored only in the memory of a running program is called “volatile”, because it vaporizes when the program ends.


Data that persists after the program that created it ends is called “persistent”. In general, files stored in a file system are persistent, as well as data stored in databases.


A simple way to make data persistent is to store it in a file. Before the program ends, it could translate its data structures into a format like JSON ([http://thinkdast.com/json](http://thinkdast.com/json)) and then write them into a file. When it starts again, it could read the file and rebuild the data structures.

But there are several problems with this solution:



1. 
Reading and writing large data structures (like a Web index) would be
slow.

1. 
The entire data structure might not fit into the memory of a single
running program.

1. 
If a program ends unexpectedly (for example, due to a power outage),
any changes made since the program last started would be lost.


A better alternative is a database that provides persistent storage and the ability to read and write parts of the database without reading and writing the whole thing.


There are many kinds of database management systems (DBMS) that provide different capabilities. You can read an overview at [http://thinkdast.com/database](http://thinkdast.com/database).


The database I recommend for this exercise is Redis, which provides persistent data structures that are similar to Java data structures. Specifically, it provides:



* 
Lists of strings, similar to Java `List`.

* 
Hashes, similar to Java `Map`.

* 
Sets of strings, similar to Java `Set`.


Redis is a “key-value database”, which means that the data structures it contains (the values) are identified by unique strings (the keys). A key in Redis plays the same role as a reference in Java: it identifies an object. We'll see some examples soon.