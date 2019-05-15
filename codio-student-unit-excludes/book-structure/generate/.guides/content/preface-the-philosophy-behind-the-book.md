Data structures and algorithms are among the most important inventions of the last 50 years, and they are fundamental tools software engineers need to know.  But in my opinion, most of the books on these topics are too theoretical, too big, and too “bottom up”:

* **Too theoretical**  Mathematical analysis of algorithms is based
on simplifying assumptions that limit its usefulness in practice.
Many presentations of this topic gloss over the simplifications and
focus on the math.  In this book I present the most practical subset
of this material and omit or de-emphasize the rest.

* **Too big** Most books on these topics are at least 500 pages,
and some are more than 1000.  By focusing on the topics I think are
most useful for software engineers, I kept this book under
200 pages.

* **Too “bottom up”** Many data structures books focus on how data
structures work (the implementations), with less about how to use
them (the interfaces).  In this book, I go “top down”, starting
with the interfaces.  Readers learn to use the structures in the
Java Collections Framework before getting into the details of how
they work.


Finally, some books present this material out of context and without motivation: it's just one damn data structure after another! I try to liven it up by organizing the topics around an application --- web search --- that uses data structures extensively, and is an interesting and important topic in its own right.


This application motivates some topics that are not usually covered in an introductory data structures class, including persistent data structures with Redis.


I have made difficult decisions about what to leave out, but  I have made some compromises.  I include a few topics that most readers will never use, but that they might be expected to know, possibly in a technical interview.  For these topics, I present both the conventional wisdom as well as my reasons to be skeptical. 

This book also presents basic aspects of software engineering practice, including version control and unit testing.  Most chapters include an exercise that allows readers to apply what they have learned. Each exercise provides automated tests that check the solution. And for most exercises, I present my solution at the beginning of the next chapter.