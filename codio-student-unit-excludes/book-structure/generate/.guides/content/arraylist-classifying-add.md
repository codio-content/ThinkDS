Here's a version of `add` that takes an index and an element as parameters:

```code
    public void add(int index, E element) {
        if (index < 0 || index > size) {
            throw new IndexOutOfBoundsException();
        }
        // add the element to get the resizing
        add(element);
        
        // shift the other elements
        for (int i=size-1; i>index; i--) {
            array[i] = array[i-1];
        }
        // put the new one in the right place
        array[index] = element;
    }
```

This two-parameter version, called `add(int, E)`, uses the one-parameter version, called `add(E)`, which puts the new element at the end. Then it shifts the other elements to the right, and puts the new element in the correct place.


Before we can classify the two-parameter `add(int, E)`, we have to classify the one-parameter `add(E)`:

```code
    public boolean add(E element) {
        if (size >= array.length) {
            // make a bigger array and copy over the elements
            E[] bigger = (E[]) new Object[array.length * 2];
            System.arraycopy(array, 0, bigger, 0, array.length);
            array = bigger;
        } 
        array[size] = element;
        size++;
        return true;
    }
```

The one-parameter version turns out to be hard to analyze. If there is an unused space in the array, it is constant time, but if we have to resize the array, it's linear because `System.arraycopy` takes time proportional to the size of the array. 


So is `add` constant time or linear? We can classify this method by thinking about the average number of operations per add over a series of $n$ adds. For simplicity, assume we start with an array that has room for 2 elements.



* 
The first time we call add, it finds unused space in the array, so it
stores 1 element.

* 
The second time, it finds unused space in the array, so it stores 1
element.

* 
The third time, we have to resize the array, copy 2 elements, and
store 1 element. Now the size of the array is 4.

* 
The fourth time stores 1 element.

* 
The fifth time resizes the array, copies 4 elements, and stores 1
element. Now the size of the array is 8.

* 
The next 3 adds store 3 elements.

* 
The next add copies 8 and stores 1. Now the size is 16.

* 
The next 7 adds store 7 elements.


And so on. Adding things up:



* 
After 4 adds, we've stored 4 elements and copied 2.

* 
After 8 adds, we've stored 8 elements and copied 6.

* 
After 16 adds, we've stored 16 elements and copied 14.


By now you should see the pattern: to do $n$ adds, we have to store $n$ elements and copy $n-2$. So the total number of operations is $n + n - 2$, which is $2n-2$.

To get the average number of operations per add, we divide the total by $n$; the result is $2 - 2/n$. As $n$ gets big, the second term, $2/n$, gets small. Invoking the principle that we only care about the largest exponent of $n$, we can think of `add` as constant time.


It might seem strange that an algorithm that is sometimes linear can be constant time on average. The key is that we double the length of the array each time it gets resized. That limits the number of times each element gets copied. Otherwise --- if we add a fixed amount to the length of the array, rather than multiplying by a fixed amount --- the analysis doesn't work.




This way of classifying an algorithm, by computing the average time in a series of invocations, is called **amortized analysis**.  You can read more about it at  [http://thinkdast.com/amort](http://thinkdast.com/amort).  The key idea is that the extra cost of copying the array is spread, or “amortized”, over a series of invocations.

Now, if `add(E)` is constant time, what about `add(int, E)`? After calling `add(E)`, it loops through part of the array and shifts elements. This loop is linear, except in the special case where we are adding at the end of the list. So `add(int, E)` is linear.