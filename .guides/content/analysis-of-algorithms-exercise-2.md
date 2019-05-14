The exercise for this chapter is to implement a `List` that uses a Java array to store the elements. 

If you look in the two tabs to the left, you'll find the source files you need:


{Run Test|assessment}(test-1977323988)




*  `MyArrayList.java` contains a partial implementation of the
`List` interface.  Four of the methods are incomplete; your job
is to fill them in.

*  `MyArrayListTest.java` contains JUnit tests you can use to
check your work.




When you run the tests, several of them should fail. If you examine the source code, you'll find four `TODO` comments indicating the methods you should fill in. {Run Test!}(sh .guides/bg.sh javac code/MyArrayListTest.java java -cp code/ MyArrayListTest )


Before you start filling in the missing methods, let's walk through some of the code. Here are the class definition, instance variables, and constructor.



```code
public class MyArrayList<E> implements List<E> {
    int size;                    // keeps track of the number of elements
    private E[] array;           // stores the elements
    
    public MyArrayList() {
        array = (E[]) new Object[10];
        size = 0;
    }
}
```

As the comments indicate, `size` keeps track of how many elements are in `MyArrayList`, and `array` is the array that actually contains the elements.


The constructor creates an array of 10 elements, which are initially `null`, and sets `size` to 0. Most of the time, the length of the array is bigger than `size`, so there are unused slots in the array.


One detail about Java: you can't instantiate an array using a type parameter; for example, the following will not work:

```code
        array = new E[10];
```

To work around this limitation, you have to instantiate an array of `Object` and then typecast it. You can read more about this issue at [http://thinkdast.com/generics](http://thinkdast.com/generics).

Next we'll look at the method that adds elements to the list:

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

If there are no unused spaces in the array, we have to create a bigger array and copy over the elements. Then we can store the element in the array and increment `size`.


It might not be obvious why this method returns a boolean, since it seems like it always returns `true`. As always, you can find the answer in the documentation: [http://thinkdast.com/colladd](http://thinkdast.com/colladd). It's also not obvious how to analyze the performance of this method. In the normal case, it's constant time, but if we have to resize the array, it's linear. I'll explain how to handle this in Section 3.2.


Finally, let's look at `get`; then you can get started on the exercises.

```code
    public T get(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException();
        }
        return array[index];
    }
```

Actually, `get` is pretty simple: if the index is out of bounds, it throws an exception; otherwise it reads and returns an element of the array. Notice that it checks whether the index is less than `size`, not `array.length`, so it's not possible to access the unused elements of the array.


In `MyArrayList.java`, you'll find a stub for `set` that looks like this:

```code
    public T set(int index, T element) {
        // TODO: fill in this method.
        return null;
    }
```

Read the documentation of `set` at [http://thinkdast.com/listset](http://thinkdast.com/listset), then fill in the body of this method. If you run `MyArrayListTest` again, `testSet` should pass.


HINT: Try to avoid repeating the index-checking code.

Your next mission is to fill in `indexOf`. As usual, you should read the documentation at [http://thinkdast.com/listindof](http://thinkdast.com/listindof) so you know what it's supposed to do. In particular, notice how it is supposed to handle `null`.


I've provided a helper method called `equals` that compares an element from the array to a target value and returns `true` if they are equal (and it handles `null` correctly). Notice that this method is private because it is only used inside this class; it is not part of the `List` interface.


When you are done, run `MyArrayListTest` again; `testIndexOf` should pass now, as well as the other tests that depend on it. {Run Test!}(sh .guides/bg.sh javac code/MyArrayListTest.java java -cp code/ MyArrayListTest )


Only two more methods to go, and you'll be done with this exercise. The next one is an overloaded version of `add` that takes an index and stores the new value at the given index, shifting the other elements to make room, if necessary.


Again, read the documentation at [http://thinkdast.com/listadd](http://thinkdast.com/listadd), write an implementation, and run the tests for confirmation.

HINT: Avoid repeating the code that makes the array bigger.

Last one: fill in the body of `remove`.  The documentation is at [http://thinkdast.com/listrem](http://thinkdast.com/listrem). When you finish this one, all tests should pass.


Once you have your implementation working, compare it to mine, which you can read at [http://thinkdast.com/myarraylist](http://thinkdast.com/myarraylist).