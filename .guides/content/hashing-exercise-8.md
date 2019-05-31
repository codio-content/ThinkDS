In this exercise, you will finish off the implementation of `MyBetterMap`.  In the repository for this book, you'll find the source files for this exercise:



*  `MyLinearMap.java` contains our solution to the previous exercise, which we will build on in this exercise.
*  `MyBetterMap.java` contains the code from the previous chapter with some methods you will fill in.
*  `MyHashMap.java` contains the outline of a hash table that grows when needed, which you will complete.
*  `MyLinearMapTest.java` contains the unit tests for `MyLinearMap`.
*  `MyBetterMapTest.java` contains the unit tests for `MyBetterMap`.
*  `MyHashMapTest.java` contains the unit tests for `MyHashMap`.
*  `Profiler.java` contains code for measuring and plotting runtime versus problem size.
*  `ProfileMapPut.java` contains code that profiles the `Map.put` method. 

{Check It!|assessment}(test-617588014)

Several tests should fail, because you have some work to do!




Review the implementation of `put` and `get` from the previous chapter. Then fill in the body of `containsKey`. HINT: use `chooseMap`. Run `ant MyBetterMapTest` again and confirm that `testContainsKey` passes.


Fill in the body of `containsValue`. HINT: *don't* use `chooseMap`.  Run `ant MyBetterMapTest` again and confirm that `testContainsValue` passes. Notice that we have to do more work to find a value than to find a key.

Like `put` and `get`, this implementation of `containsKey` is linear, because it has to search one of the embedded sub-maps.  In the next chapter, we'll see how we can improve this implementation even more.