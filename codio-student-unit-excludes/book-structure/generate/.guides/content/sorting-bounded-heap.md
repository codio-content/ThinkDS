A bounded heap is a heap that is limited to contain at most $k$ elements. If you have $n$ elements, you can keep track of the $k$ largest elements like this:

Initially, the heap is empty.  For each element, `x`:



*  Branch 1: If the heap is not full, add `x` to the heap.
*  Branch 2: If the heap is full, compare `x` to the *smallest* element in the heap. If `x` is smaller, it cannot be one of the largest $k$ elements, so you can discard it.
*  Branch 3: If the heap is full and `x` is greater than the smallest element in the heap, remove the smallest element from the heap and add `x`. 


Using a heap with the smallest element at the top, we can keep track of the largest $k$ elements. Let's analyze the performance of this algorithm. For each element, we perform one of:



*  Branch 1: Adding an element to the heap is $O(\log k)$.
*  Branch 2: Finding the smallest element in the heap is $O(1)$.
*  Branch 3: Removing the smallest element is $O(\log k)$. Adding `x` is also $O(\log k)$. 

In the worst case, if the elements appear in ascending order, we always run Branch 3. In that case, the total time to process $n$ elements is $O(n \log k)$, which is linear in $n$.



In `ListSorter.java` you'll find the outline of a method called `topK` that takes a `List`, a `Comparator`, and an integer $k$. It should return the $k$ largest elements in the `List` in ascending order. Fill it in and then run `ListSorterTest`

{Check It!|assessment}(test-2358547291)
