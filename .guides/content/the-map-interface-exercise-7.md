In the repository for this book, you'll find the source files for this exercise:



*  `MyLinearMap.java` contains starter code for the first part
of the exercise.

*  `MyLinearMapTest.java` contains the unit tests for
`MyLinearMap`.


You'll also find the Ant build file `build.xml`.


Run `ant build` to compile the source files. Then run `ant   MyLinearMapTest`; several tests should fail, because you have some work to do!


First, fill in the body of `findEntry`. This is a helper method that is not part of the `Map` interface, but once you get it working, you can use it for several methods. Given a target key, it should search through the entries and return the entry that contains the target (as a key, not a value) or `null` if it's not there. Notice that I provide an `equals` method that compares two keys and handles `null` correctly.


You can run `ant MyLinearMapTest` again, but even if your `findEntry` is correct, the tests won't pass because `put` is not complete.


Fill in `put`. You should read the documentation of `Map.put` at [http://thinkdast.com/listput](http://thinkdast.com/listput) so you know what it is supposed to do. You might want to start with a version of `put` that always adds a new entry and does not modify an existing entry; that way you can test the simple case first.  Or if you feel more confident, you can write the whole thing at once.


Once you've got `put` working, the test for `containsKey` should pass.

Read the documentation of `Map.get` at   [http://thinkdast.com/listget](http://thinkdast.com/listget)   and then fill in the method. Run the tests again.

Finally, read the documentation of `Map.remove` at   [http://thinkdast.com/maprem](http://thinkdast.com/maprem)   and fill in the method.

At this point, all tests should pass. Congratulations!