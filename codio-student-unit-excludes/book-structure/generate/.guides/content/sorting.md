Computer science departments have an unhealthy obsession with sort algorithms. Based on the amount of time CS students spend on the topic, you would think that choosing sort algorithms is the cornerstone of modern software engineering. Of course, the reality is that software developers can go years, or entire careers, without thinking about how sorting works. For almost all applications, they use whatever general-purpose algorithm is provided by the language or libraries they use. And usually that's just fine.


So if you skip this chapter and learn nothing about sort algorithms, you can still be an excellent developer. But there are a few reasons you might want to do it anyway:



1.  Although there are general-purpose algorithms that work well for the vast majority of applications, there are two special-purpose algorithms you might need to know about: radix sort and bounded heap sort.
1.  One sort algorithm, merge sort, makes an excellent teaching example because it demonstrates an important and useful strategy for algorithm design, called “divide-conquer-glue”. Also, when we analyze its performance, you will learn about an order of growth we have not seen before, **linearithmic**. Finally, some of the most widely-used algorithms are hybrids that include elements of merge sort.
1.  One other reason to learn about sort algorithms is that technical interviewers love to ask about them. If you want to get hired, it helps if you can demonstrate CS cultural literacy. 

So, in this chapter we'll analyze insertion sort, you will implement merge sort, I'll tell you about radix sort, and you will write a simple version of a bounded heap sort.