Before I explain the iterative version of DFS, I'll explain the stack data structure.  We'll start with the general concept of a stack, which I'll call a “stack” with a lowercase “s”. Then we'll talk about two Java `interfaces` that define stack methods: `Stack` and `Deque`.



A stack is a data structure that is similar to a list: it is a collection that maintains the order of the elements. The primary difference between a stack and a list is that the stack provides fewer methods. In the usual convention, it provides:



*  `push`: which adds an element to the top of the stack.
*  `pop`: which removes and returns the top-most element from the stack.
*  `peek`: which returns the top-most element without modifying the stack.
*  `isEmpty`: which indicates whether the stack is empty. 

Because `pop` always returns the top-most element, a stack is also called a “LIFO”, which stands for “last in, first out”. An alternative to a stack is a “queue”, which returns elements in the same order they are added; that is, “first in, first out”, or FIFO.


It might not be obvious why stacks and queues are useful: they don't provide any capabilities that aren't provided by lists; in fact, they provide fewer capabilities. So why not use lists for everything? There are two reasons:



1.  If you limit yourself to a small set of methods --- that is, a small API --- your code will be more readable and less error-prone. For example, if you use a list to represent a stack, you might accidentally remove an element in the wrong order. With the stack API, this kind of mistake is literally impossible. And the best way to avoid errors is to make them impossible.
1.  If a data structure provides a small API, it is easier to implement efficiently. For example, a simple way to implement a stack is a singly-linked list. When we push an element onto the stack, we add it to the beginning of the list; when we pop an element, we remove it from the beginning. For a linked list, adding and removing from the beginning are constant time operations, so this implementation is efficient. Conversely, big APIs are harder to implement efficiently. 


To implement a stack in Java, you have three options:



1.  Go ahead and use `ArrayList` or `LinkedList`. If you use `ArrayList`, be sure to add and remove from the *end*, which is a constant time operation. And be careful not to add elements in the wrong place or remove them in the wrong order.
1.  Java provides a class called `Stack` that provides the standard set of stack methods. But this class is an old part of Java: it is not consistent with the Java Collections Framework, which came later.
1.  Probably the best choice is to use one of the implementations of the `Deque` interface, like `ArrayDeque`. 

“Deque” stands for “double-ended queue”; it's supposed to be pronounced “deck”, but some people say “deek”. In Java, the `Deque` interface provides `push`, `pop`, `peek`, and `isEmpty`, so you can use a `Deque` as a stack. It provides other methods, which you can read about at [http://thinkdast.com/deque](http://thinkdast.com/deque), but we won't use them for now.