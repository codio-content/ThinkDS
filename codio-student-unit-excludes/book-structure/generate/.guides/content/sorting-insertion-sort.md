We'll start with insertion sort, mostly because it is simple to describe and implement. It is not very efficient, but it has some redeeming qualities, as we'll see.


Rather than explain the algorithm here, I suggest you read the insertion sort Wikipedia page at [http://thinkdast.com/insertsort](http://thinkdast.com/insertsort), which includes pseudocode and animated examples. Come back when you get the general idea.

Here's an implementation of insertion sort in Java:

```code
public class ListSorter<T> {

    public void insertionSort(List<T> list, Comparator<T> comparator) {

        for (int i=1; i < list.size(); i++) {
            T elt_i = list.get(i);
            int j = i;
            while (j > 0) {
                T elt_j = list.get(j-1);
                if (comparator.compare(elt_i, elt_j) >= 0) {
                    break;
                }
                list.set(j, elt_j);
                j--;
            }
            list.set(j, elt_i);
        }
    }
}
```

I define a class, `ListSorter`, as a container for sort algorithms. By using the type parameter, `T`, we can write methods that work on lists containing any object type.


`insertionSort` takes two parameters, a `List` of any kind and a `Comparator` that knows how to compare type `T` objects. It sorts the list “in place”, which means it modifies the existing list and does not have to allocate any new space.


The following example shows how to call this method with a `List` of `Integer` objects:

```code
        List<Integer> list = new ArrayList<Integer>(
            Arrays.asList(3, 5, 1, 4, 2));

        Comparator<Integer> comparator = new Comparator<Integer>() {
            @Override
            public int compare(Integer elt1, Integer elt2) {
                return elt1.compareTo(elt2);
            }
        };

        ListSorter<Integer> sorter = new ListSorter<Integer>();
        sorter.insertionSort(list, comparator);
        System.out.println(list);
```

`insertionSort` has two nested loops, so you might guess that its runtime is quadratic. In this case, that turns out to be correct, but before you jump to that conclusion, you have to check that the number of times each loop runs is proportional to $n$, the size of the array.


The outer loop iterates from 1 to `list.size()`, so it is linear in the size of the list, $n$. The inner loop iterates from `i` to 0, so it is also linear in $n$. Therefore, the total number of times the inner loop runs is quadratic.


If you are not sure about that, here's the argument:



* 
The first time through, $i=1$ and the inner loop runs at most
once.

* 
The second time, $i=2$ and the inner loop runs at most twice.

* 
The last time, $i=n-1$ and the inner loop runs at most
$n-1$ times.


So the total number of times the inner loop runs is the sum of the series $1, 2, \ldots , n-1$, which is $n (n-1) / 2$. And the leading term of that expression (the one with the highest exponent) is $n^2$.


In the worst case, insertion sort is quadratic. However:



1. 
If the elements are already sorted, or nearly so, insertion sort is
linear. Specifically, if each element is no more than $k$
locations away from where it should be, the inner loop never runs more
than $k$ times, and the total runtime is $O(kn)$.

1. 
Because the implementation is simple, the overhead is low; that is,
although the runtime is $a n^2$, the coefficient of the leading
term, $a$, is probably small.


So if we know that the array is nearly sorted, or is not very big, insertion sort might be a good choice. But for large arrays, we can do better. In fact, much better.