In the repository for this book you'll find the source files you need for this exercise:



1.  `Profiler.java` contains the implementation of the `Profiler` class described above. You will use this class, but you don't have to know how it works. But feel free to read the source.
1.  `ProfileListAdd.java` contains starter code for this exercise, including the example, above, which profiles `ArrayList.add`. You will modify this file to profile a few other methods. 


Also, in the `code` directory , you'll find the Ant build file `build.xml`.

Run `ant ProfileListAdd` to run `ProfileListAdd.java`. You should get results similar to Figure 4.1, but you might have to adjust `startN` or `endMillis`. The estimated slope should be close to 1, indicating that performing $n$ add operations takes time proportional to $n$ raised to the exponent 1; that is, it is in $O(n)$.

In `ProfileListAdd.java`, you'll find an empty method named `profileArrayListAddBeginning`. Fill in the body of this method with code that tests `ArrayList.add`, always putting the new element at the beginning. If you start with a copy of `profileArrayListAddEnd`, you should only have to make a few changes. Add a line in `main` to invoke this method.

Run `ant ProfileListAdd` again and interpret the results. Based on our understanding of how `ArrayList` works, we expect each add operation to be linear, so the total time for $n$ adds should be quadratic. If so, the estimated slope of the line, on a log-log scale, should be near 2. Is it?


Now let's compare that to the performance of `LinkedList`. Fill in the body of `profileLinkedListAddBeginning` and use it to classify `LinkedList.add` when we put the new element at the beginning. What performance do you expect? Are the results consistent with your expectations?


Finally, fill in the body of `profileLinkedListAddEnd` and use it to classify `LinkedList.add` when we put the new element at the end. What performance do you expect? Are the results consistent with your expectations?

I'll present results and answer these questions in the next chapter.