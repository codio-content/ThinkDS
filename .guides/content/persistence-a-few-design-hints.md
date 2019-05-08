Now you *really* have all the information you need; you should start working on the exercise. But if you get stuck, or if you really don't know how to get started, you can come back for a few more hints.

**Don't read the following until you have run the test code, tried out some basic Redis commands, and written a few methods in `JedisIndex.java**`.

OK, if you are really stuck, here are some methods you might want to work on:

```code
    /**
     * Adds a URL to the set associated with term.
     */
    public void add(String term, TermCounter tc) {}

    /**
     * Looks up a search term and returns a set of URLs.
     */
    public Set<String> getURLs(String term) {}

    /**
     * Returns the number of times the given term appears at the given URL.
     */
    public Integer getCount(String url, String term) {}

    /**
     * Pushes the contents of the TermCounter to Redis.
     */
    public List<Object> pushTermCounterToRedis(TermCounter tc) {}
```

These are the methods I used in my solution, but they are certainly not the only way to divide things up. So please take these suggestions if they help, but ignore them if they don't.

For each method, consider writing the tests first. When you figure out how to test a method, you often get ideas about how to write it.

Good luck!