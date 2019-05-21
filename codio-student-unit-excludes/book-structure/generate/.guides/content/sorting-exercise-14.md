Merge sort is one of several algorithms whose runtime is better than quadratic. Again, rather than explaining the algorithm here, I suggest you read about it on Wikipedia at [http://thinkdast.com/mergesort](http://thinkdast.com/mergesort).  Once you get the idea, come back and you can test your understanding by writing an implementation.


In the repository for this book, you'll find the source files for this exercise:



*  `ListSorter.java`
*  `ListSorterTest.java` 

Run `ant build` to compile the source files, then run `ant ListSorterTest`. As usual, it should fail, because you have work to do.


In `ListSorter.java`, I've provided an outline of two methods, `mergeSortInPlace` and `mergeSort`:

```code
    public void mergeSortInPlace(List<T> list, Comparator<T> comparator) {
        List<T> sorted = mergeSortHelper(list, comparator);
        list.clear();
        list.addAll(sorted);
    }

    private List<T> mergeSort(List<T> list, Comparator<T> comparator) {
       // TODO: fill this in!
       return null;
    }
```

These two methods do the same thing but provide different interfaces. `mergeSort` takes a list and returns a new list with the same elements sorted in ascending order. `mergeSortInPlace` is a `void` method that modifies an existing list.


Your job is to fill in `mergeSort`. Before you write a fully recursive version of merge sort, start with something like this:



1.  Split the list in half.
1.  Sort the halves using `Collections.sort` or `insertionSort`.
1.  Merge the sorted halves into a complete sorted list. 

This will give you a chance to debug the merge code without dealing with the complexity of a recursive method.


Next, add a base case (see [http://thinkdast.com/basecase](http://thinkdast.com/basecase)). If you are given a list with only one element, you could return it immediately, since it is already sorted, sort of. Or if the length of the list is below some threshold, you could sort it using `Collections.sort` or `insertionSort`. Test the base case before you proceed.

Finally, modify your solution so it makes two recursive calls to sort the halves of the array. When you get it working, `testMergeSort` and `testMergeSortInPlace` should pass.