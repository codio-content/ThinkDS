The Java Collections Framework (JCF) defines an `interface` called `List` and provides two implementations, `ArrayList` and `LinkedList`.


The `interface` defines what it means to be a `List`; any class that implements this `interface` has to provide a particular set of methods, including `add`, `get`, `remove`, and about 20 more.

`ArrayList` and `LinkedList` provide these methods, so they can be used interchangeably. A method written to work with a `List` will work with an `ArrayList`, `LinkedList`, or any other object that implements `List`.



See the contrived example that demonstrates the point in the panel to the left.
[Open Visualizer](open_tutor code/ListClientExample.java panel=0)


`ListClientExample` doesn't do anything useful, but it has the essential elements of a class that **encapsulates** a `List`; that is, it contains a `List` as an instance variable.  I'll use this class to make a point, and then you'll work with it in the first exercise.


The `ListClientExample` constructor initializes `list` by **instantiating** (that is, creating) a new `LinkedList`; the getter method called `getList` returns a reference to the internal `List` object; and `main` contains a few lines of code to test these methods.

The important thing about this example is that it uses `List` whenever possible and avoids specifying `LinkedList` or `ArrayList` unless it is necessary. For example, the instance variable is declared to be a `List`, and `getList` returns a `List`, but neither specifies which kind of list.

If you change your mind and decide to use an `ArrayList`, you only have to change the constructor; you don't have to make any other changes.


This style is called **interface-based programming**, or more casually, “programming to an interface” (see [http://thinkdast.com/interbaseprog](http://thinkdast.com/interbaseprog)). Here we are talking about the general idea of an interface, not a Java `interface`.

When you use a library, your code should only depend on the interface, like `List`.  It should not depend on a specific implementation, like `ArrayList`. That way, if the implementation changes in the future, the code that uses it will still work.

On the other hand, if the interface changes, the code that depends on it has to change, too.  That's why library developers avoid changing interfaces unless absolutely necessary.