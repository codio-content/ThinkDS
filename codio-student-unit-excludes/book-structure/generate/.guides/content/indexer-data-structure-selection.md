The fundamental operation of the index is a **lookup**; specifically, we need the ability to look up a term and find all pages that contain it. The simplest implementation would be a collection of pages. Given a search term, we could iterate through the contents of the pages and select the ones that contain the search term. But the runtime would be proportional to the total number of words on all the pages, which would be way too slow.


A better alternative is a **map**, which is a data structure that represents a collection of **key-value pairs** and provides a fast way to look up a **key** and find the corresponding **value**. For example, the first map we'll construct is a `TermCounter`, which maps from each search term to the number of times it appears in a page. The keys are the search terms and the values are the counts (also called “frequencies”).

Java provides an interface called `Map` that specifies the methods a map should provide; the most important are:



* 
`get(key)`: This method looks up a key and returns the
corresponding value.

* 
`put(key, value)`: This method adds a new key-value pair to the
`Map`, or if the key is already in the map, it replaces the
value associated with `key`.


Java provides several implementations of `Map`, including the two we will focus on, `HashMap` and `TreeMap`. In upcoming chapters, we'll look at these implementations and analyze their performance.

In addition to the `TermCounter`, which maps from search terms to counts, we will define a class called `Index`, which maps from a search term to a collection of pages where it appears. And that raises the next question, which is how to represent a collection of pages. Again, if we think about the operations we want to perform, that guides our decision.


In this case, we'll need to combine two or more collections and find the pages that appear in all of them. You might recognize this operation as **set intersection**: the intersection of two sets is the set of elements that appear in both.

As you might expect by now, Java provides a `Set` interface that defines the operations a set should perform. It doesn't actually provide set intersection, but it provides methods that make it possible to implement intersection and other set operations efficiently. The core `Set` methods are:



* 
`add(element)`: This method adds an element to a set; if the
element is already in the set, it has no effect.

* 
`contains(element)`: This method checks whether the given
element is in the set.


Java provides several implementations of `Set`, including `HashSet` and `TreeSet`.


Now that we've designed our data structures from the top down, we'll implement them from the inside out, starting with `TermCounter`.