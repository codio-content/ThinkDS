For many methods, we can identify the order of growth by examining the code. For example, here's the implementation of `get` from `MyArrayList`:

```code
    public E get(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException();
        }
        return array[index];
    }
```
[Highlight in Code](open_file code/MyArrayList.java panel=0 ref="public E get" count=6)


Everything in `get` is constant time, so `get` is constant time. No problem.


Now that we've classified `get`, we can classify `set`, which uses it. Here is our implementation of `set` from the previous exercise:

```code
    public E set(int index, E element) {
        E old = get(index);
        array[index] = element;
        return old;
    }
```
[Highlight in Code](open_file code/MyArrayList.java panel=0 ref="public E set" count=5)


One slightly clever part of this solution is that it does not check the bounds of the array explicitly; it takes advantage of `get`, which raises an exception if the index is invalid.


Everything in `set`, including the invocation of `get`, is constant time, so `set` is also constant time.


Next we'll look at some linear methods. For example, here's my implementation of `indexOf`:

```code
    public int indexOf(Object target) {
        for (int i = 0; i<size; i++) {
            if (equals(target, array[i])) {
                return i;
            }
        }
        return -1;
    }
```
[Highlight in Code](open_file code/MyArrayList.java panel=0 ref="public int indexOf" count=8)


Each time through the loop, `indexOf` invokes `equals`, so we have to classify `equals` first. Here it is:

```code
    private boolean equals(Object target, Object element) {
        if (target == null) {
            return element == null;
        } else {
            return target.equals(element);
        }
    }
```
[Highlight in Code](open_file code/MyArrayList.java panel=0 ref="private boolean equals" count=7)


This method invokes `target.equals`; the runtime of this method might depend on the size of `target` or `element`, but it probably doesn't depend on the size of the array, so we consider it constant time for purposes of analyzing `indexOf`.


Getting back to `indexOf`, everything inside the loop is constant time, so the next question we have to consider is: how many times does the loop execute?

If we get lucky, we might find the target object right away and return after testing only one element. If we are unlucky, we might have to test all of the elements. On average, we expect to test half of the elements, so this method is considered linear (except in the unlikely case that we know the target element is at the beginning of the array).


The analysis of `remove` is similar. Here's my implementation:

```code
    public E remove(int index) {
        E element = get(index);
        for (int i=index; i<size-1; i++) {
            array[i] = array[i+1];
        }
        size--;
        return element;
    }
```
[Highlight in Code](open_file code/MyArrayList.java panel=0 ref="public E remove" count=8)


It uses `get`, which is constant time, and then loops through the array, starting from `index`. If we remove the element at the end of the list, the loop never runs and this method is constant time. If we remove the first element, we loop through all of the remaining elements, which is linear. So, again, this method is considered linear (except in the special case where we know the element is at the end or a constant distance from the end).