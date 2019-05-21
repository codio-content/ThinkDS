During the 2008 United States Presidential Campaign, candidate Barack Obama was asked to perform an impromptu algorithm analysis when he visited Google. Chief executive Eric Schmidt jokingly asked him for “the most efficient way to sort a million 32-bit integers.” Obama had apparently been tipped off, because he quickly replied, “I think the bubble sort would be the wrong way to go.” You can watch the video at [http://thinkdast.com/obama](http://thinkdast.com/obama).

Obama was right: bubble sort is conceptually simple but its runtime is quadratic; and even among quadratic sort algorithms, its performance is not very good.  See [http://thinkdast.com/bubble](http://thinkdast.com/bubble).


The answer Schmidt was probably looking for is “radix sort”, which is a **non-comparison** sort algorithm that works if the size of the elements is bounded, like a 32-bit integer or a 20-character string.


To see how this works, imagine you have a stack of index cards where each card contains a three-letter word. Here's how you could sort the cards:



1.  Make one pass through the cards and divide them into buckets based on the first letter. So words starting with `a` should be in one bucket, followed by words starting with `b`, and so on.
1.  Divide each bucket again based on the second letter. So words starting with `aa` should be together, followed by words starting with `ab`, and so on. Of course, not all buckets will be full, but that's OK.
1.  Divide each bucket again based on the third letter. 

At this point each bucket contains one element, and the buckets are sorted in ascending order. Figure 17.3 shows an example with three-letter words.

![Figure 17.3 Example of radix sort with three-letter words.](figs/radix_sort1.jpg)

**Figure 17.3 Example of radix sort with three-letter words.**

The top row shows the unsorted words. The second row shows what the buckets look like after the first pass. The words in each bucket begin with the same letter.

After the second pass, the words in each bucket begin with the same two letters. After the third pass, there can be only one word in each bucket, and the buckets are in order.

During each pass, we iterate through the elements and add them to buckets. As long as the buckets allow addition in constant time, each pass is linear.


The number of passes, which I'll call $w$, depends on the “width” of the words, but it doesn't depend on the number of words, $n$. So the order of growth is $O(wn)$, which is linear in $n$.

There are many variations on radix sort, and many ways to implement each one. You can read more about them at [http://thinkdast.com/radix](http://thinkdast.com/radix). As an optional exercise, consider writing a version of radix sort.