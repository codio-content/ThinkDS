In the repository for this book, you'll find the source files for this exercise:



*  `JedisMaker.java` contains example code for connecting to a Redis server and running a few Jedis methods.
*  `JedisIndex.java` contains starter code for this exercise.
*  `JedisIndexTest.java` contains test code for `JedisIndex`.
*  `WikiFetcher.java` contains the code we saw in previous exercises to read web pages and parse them using jsoup. 

You will also need these files, which you worked on in previous exercises:



*  `Index.java` implements an index using Java data structures.
*  `TermCounter.java` represents a map from terms to their frequencies.
*  `WikiNodeIterable.java` iterates through the nodes in a DOM tree produced by jsoup. 

If you have working versions of these files, you can use them for this exercise.  If you didn't do the previous exercises, or you are not confident in your solutions, you can copy my solutions from the `solutions` folder.

The first step is to use Jedis to connect to your Redis server. `RedisMaker.java` shows how to do this. It reads information about your Redis server from a file, connects to it and logs in using your password, then returns a `Jedis` object you can use to perform Redis operations.


If you open `JedisMaker.java`, you should see the `JedisMaker` class, which is a helper class that provides one static method, `make`, which creates a `Jedis` object. Once this object is authenticated, you can use it to communicate with your Redis database. 
`JedisMaker` reads information about your Redis server from a file named `redis_url.txt`.

Run the `JedisMaker` example code ([Highlight](open_file code/JedisMaker.java panel=0 ref="public static void main" count=27)) using the button below:

{Run! | terminal}(cd code && javac JedisIndex.java JedisMaker.java WikiFetcher.java && java -cp lib/*:. JedisMaker && cd ../ )



This example demonstrates the data types and methods you are most likely to use for this exercise. When you run it, the output should be:

```code
Got value: myvalue
element2 is member: true
element at index 1: element2
frequency of word1: 2
frequency of word2: 1
```

In the next section, I'll explain how the code works.