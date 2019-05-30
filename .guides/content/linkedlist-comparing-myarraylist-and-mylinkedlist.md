The following table summarizes the differences between `MyLinkedList` and `MyArrayList`, where `1` means $O(1)$ or constant time and $n$ means $O(n)$ or linear.

||MyArrayList|MyLinkedList |
|-|-|-|
|add (at the end)|**1**|n|
|add (at the beginning)|n|**1**|
|add (in general)|n|n|
|get / set|**1**|n|
|indexOf / lastIndexOf|n|n|
|isEmpty / size|1|1|
|remove (from the end)|**1**|n|
|remove (from the beginning)|n|**1**|
|remove (in general)|n|n|


The operations where `MyArrayList` has an advantage are adding at the end, removing from the end, getting and setting.

The operations where `MyLinkedList` has an advantage are adding at the beginning and removing from the beginning.

For the other operations, the two implementations are in the same order of growth.


Which implementation is better? It depends on which operations you are likely to use the most. And that's why Java provides more than one implementation, because it depends.