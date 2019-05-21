My implementation of `indexOf` is below. Read through it and see if you can identify its order of growth before you read the explanation.

```code
    public int indexOf(Object target) {
        Node node = head;
        for (int i=0; i<size; i++) {
            if (equals(target, node.data)) {
                return i;
            }
            node = node.next;
        }
        return -1;
    }
```

Initially `node` gets a copy of `head`, so they both refer to the same `Node`. The loop variable, `i`, counts from 0 to `size-1`.  Each time through the loop, we use `equals` to see if we've found the target. If so, we return `i` immediately. Otherwise we advance to the next `Node` in the list.

Normally we would check to make sure the next `Node` is not `null`, but in this case it is safe because the loop ends when we get to the end of the list (assuming `size` is consistent with the actual number of nodes in the list).

If we get through the loop without finding the target, we return `-1`.


So what is the order of growth for this method?



1.  Each time through the loop we invoke `equals`, which is constant time (it might depend on the size of `target` or `data`, but it doesn't depend on the size of the list). The other operations in the loop are also constant time.
1.  The loop might run $n$ times, because in the worse case, we might have to traverse the whole list. 

So the runtime of this method is proportional to the length of the list.


Next, here is my implementation of the two-parameter `add` method. Again, you should try to classify it before you read the explanation.

```code
    public void add(int index, E element) {
        if (index == 0) {
            head = new Node(element, head);
        } else {
            Node node = getNode(index-1);
            node.next = new Node(element, node.next);
        }
        size++;
    }
```

If `index==0`, we're adding the new `Node` at the beginning, so we handle that as a special case. Otherwise, we have to traverse the list to find the element at `index-1`. We use the helper method `getNode`:


```code
    private Node getNode(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException();
        }
        Node node = head;
        for (int i=0; i<index; i++) {
            node = node.next;
        }
        return node;
    }
```

`getNode` checks whether `index` is out of bounds; if so, it throws an exception. Otherwise it traverses the list and returns the requested Node.


Jumping back to `add`, once we find the right `Node`, we create the new `Node` and put it between `node` and `node.next`. You might find it helpful to draw a diagram of this operation to make sure you understand it.

So, what's the order of growth for `add`?



1.  `getNode` is similar to `indexOf`, and it is linear for the same reason.
1.  In `add`, everything before and after `getNode` is constant time. 

So all together, `add` is linear.


Finally, let's look at `remove`:

```code
    public E remove(int index) {
        E element = get(index);
        if (index == 0) {
            head = head.next;
        } else {
            Node node = getNode(index-1);
            node.next = node.next.next;
        }
        size--;
        return element;
    }
```

`remove` uses `get` to find and store the element at `index`. Then it removes the `Node` that contained it.

If `index==0`, we handle that as a special case again. Otherwise we find the node at `index-1` and modify it to skip over `node.next` and link directly to `node.next.next`. This effectively removes `node.next` from the list, and it can be garbage collected.

Finally, we decrement `size` and return the element we retrieved at the beginning.

So, what's the order of growth for `remove`? Everything in `remove` is constant time except `get` and `getNode`, which are linear. So `remove` is linear.

When people see two linear operations, they sometimes think the result is quadratic, but that only applies if one operation is nested inside the other. If you invoke one operation after the other, the runtimes add. If they are both in $O(n)$, the sum is also in $O(n)$.