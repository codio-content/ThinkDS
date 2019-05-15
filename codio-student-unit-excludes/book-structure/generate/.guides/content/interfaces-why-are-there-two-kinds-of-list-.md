When people start working with the Java Collections Framework, they are sometimes confused about `ArrayList` and `LinkedList`.  Why does Java provide two implementations of the `List` `interface`?  And how should you choose which one to use?  We will answer these questions in the next few chapters.


I'll start by reviewing `interface`s and the classes that implement them, and I'll present the idea of “programming to an interface”.


In the first few exercises, you'll implement classes similar to `ArrayList` and `LinkedList`, so you'll know how they work, and we'll see that each of them has pros and cons.  Some operations are faster or use less space with `ArrayList`; others are faster or smaller with `LinkedList`.  Which one is better for a particular application depends on which operations it performs most often.