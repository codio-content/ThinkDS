In the panes to the left, you'll find the source files you need for this exercise:


1.  `Profiler.java` contains the implementation of the `Profiler` class described above. You will use this class, but you don't have to know how it works. But feel free to read the source.
1.  `ProfileListAdd.java` contains starter code for this exercise, including the example, above, which profiles `ArrayList.add`. You will modify this file to profile a few other methods. 

{Run! | terminal}(cd code && javac Profiler.java ProfileListAdd.java && java -cp lib/*:. ProfileListAdd && cd ../ )


Use the button above to run `ProfileListAdd.java`. You should get results similar to Figure 4.1, but you might have to adjust `startN` or `endMillis`. The estimated slope should be close to 1, indicating that performing $n$ add operations takes time proportional to $n$ raised to the exponent 1; that is, it is in $O(n)$. 


In `ProfileListAdd.java`, you'll find an empty method named `profileArrayListAddBeginning`. [(Highlight)](open_file code/ProfileListAdd.java panel=2 ref="public static void profileArrayListAddBeginning" count=1) Fill in the body of this method with code that tests `ArrayList.add`, always putting the new element at the beginning. If you start with a copy of `profileArrayListAddEnd`, you should only have to make a few changes. Add a line in `main` to invoke this method. 


To stop the current process, close the window with the graph in the bottom-right panel. Run the program again using the same button above and interpret the results. 


Based on our understanding of how `ArrayList` works, we expect each add operation to be linear, so the total time for $n$ adds should be quadratic. If so, the estimated slope of the line, on a log-log scale, should be near 2. Is it?


Now let's compare that to the performance of `LinkedList`. Fill in the body of `profileLinkedListAddBeginning` [(Highlight)](open_file code/ProfileListAdd.java panel=2 ref="public static void profileLinkedListAddBeginning" count=1) and use it to classify `LinkedList.add` when we put the new element at the beginning. What performance do you expect? Are the results consistent with your expectations? 

Finally, fill in the body of `profileLinkedListAddEnd` [(Highlight)](open_file code/ProfileListAdd.java panel=2 ref="public static void profileLinkedListAddEnd" count=1) and use it to classify `LinkedList.add` when we put the new element at the end. What performance do you expect? Are the results consistent with your expectations? 


I'll present results and answer these questions in the next chapter.
