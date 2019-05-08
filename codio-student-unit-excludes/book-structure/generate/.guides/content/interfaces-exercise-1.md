Since this is the first exercise, we'll keep it simple. You will take the code from the previous section and **swap the implementation**; that is, you will replace the `LinkedList` with an `ArrayList`.  Because the code programs to an interface, you will be able to swap the implementation by changing a single line and adding an `import` statement.

If you navigate into `src/com/allendowney/thinkdast`, you'll find the source code for this exercise:



* 
`ListClientExample.java` contains the code from the previous
section.

* 
`ListClientExampleTest.java` contains a JUnit test for
`ListClientExample`.


Review `ListClientExample` and make sure you understand what it does. Then compile and run it by pressing the button below:
{Run!}(sh .guides/bg.sh javac code/ListClientExample.java java -cp code/ ListClientExample )


Review `ListClientExampleTest`. It runs one test, which creates a `ListClientExample`, invokes `getList`, and then checks whether the result is an `ArrayList`. Initially, this test will fail because the result is a `LinkedList`, not an `ArrayList`. Run this test and confirm that it fails. {Check It!|assessment}(test-958272319)


NOTE: This test makes sense for this exercise, but it is not a good example of a test. Good tests should check whether the class under test satisfies the requirements of the *interface*; they should not depend on the details of the *implementation*.


In the `ListClientExample`, replace `LinkedList` with `ArrayList`.  You might have to add an `import` statement. Compile and run `ListClientExample`. Then run the test again. With this change, the test should now pass.

To make this test pass, you only had to change `LinkedList` in the constructor; you did not have to change any of the places where `List` appears. What happens if you do?  Go ahead and replace one or more appearances of `List` with `ArrayList`. The program should still work correctly, but now it is “overspecified”. If you change your mind in the future and want to swap the interface again, you would have to change more code.

In the `ListClientExample` constructor, what happens if you replace `ArrayList` with `List`? Why can't you instantiate a `List`?