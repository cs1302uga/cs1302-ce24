# cs1302-ce24 Recursive Problems

![Approved for: Fall 2019](https://img.shields.io/badge/Approved%20for-Fall%202019-brightgreen)

<!--![Approved for: Spring 2020](https://img.shields.io/badge/Approved%20for-Spring%202020-blue)
![Instruction: Online](https://img.shields.io/badge/Instruction-Online-important)-->

> "To understand recursion, you must understand recursion"

This class exercise explores the concept of [recursion](https://github.com/cs1302uga/cs1302-ce24).

## Course-Specific Learning Outcomes
* **LO2.c:** Use recursion to solve a non-trivial problem in a software solution.
* **LO5.b:** (Partial) Utilize a build tool such as Maven or Ant to create and manage a
complex software solution involving external dependencies.
* **LO7.c:** (Partial) Use common abstract data types and structures, including lists, queues, arrays,
and stacks in solving typical problems.

## References and Prerequisites

* [CSCI 1302 Recursion Tutorial](https://github.com/cs1302uga/cs1302-tutorials/blob/master/recursion.md)

## Questions

In your notes, clearly answer the following questions. These instructions assume that you are 
logged into the Nike server. 

**NOTE:** If a step requires you to enter in a command, please provide in your notes the full 
command that you typed to make the related action happen. If context is necessary (e.g., the 
command depends on your present working directory), then please note that context as well.

### Getting Started

1. Using Maven, create a project directory for this exercise called `cs1302-ce24` with a primary 
   package called `cs1302.ce24`.

1. Change into the `cs1302-ce24` directory that you just created using Maven, then do the
   following:
   
   1. Initialize a new Git repository:
      
      ```
      $ git init
      ```
      
   1. Create a [`.gitignore`](https://git-scm.com/docs/gitignore) (hidden file) with the following contents:
   
      ```
      bin/
      doc/
      target/
      *.class
      hs_err_pid*
      *~
      \#*\#
      core.*
      ```
      
      Add and commit the `.gitignore` file to the repository.
      
   1. Update the POM so that the project works with Java 8. After that, add and commit the `pom.xml` file to 
      the repository.
   
   1. Delete the Maven-generated driver (i.e., `src/main/java/cs1302/ce24/App.java`) and the unit test files 
      (i.e., everything under `src/test/java`). We won't add the `src` folder to the repository at this time
      because it only contains empty subdirectories. Git will not track empty directories.
   
## Exercise Steps

1. Create a `cs1302.ce24.Fac` class based on code below that provides a
   recursive [Factorial](https://mathworld.wolfram.com/Factorial.html) method. You may need to add
   a package statement and necessary imports.
   
   ```java
   /**
    * Factorial convenience class.
    */
   public class Fac {

       public static void main(String[] args) {
           System.out.println(factorial(3));
       } // main

       /**
        * Returns the Factorial of {@code n}.
        * @param n index
        * @return Factorial of {@code n}
        */
       public static int factorial(int n) {
           if ((n == 0) || (n == 1)) {
               return 1;
           } // if
           return n * factorial(n - 1);
       } // fibonacci
    
   } // Fac
   ```
    
1. **Next, use Maven to compile and run the code.** Please use the `exec:java` phase to run.
   After you've confirmed that it compiles and runs, add and commit your `src` directory which
   now contains `Fac.java` in one of its subdirectories, **then tag it as `checkpoint-1.1`**.
  
![CP1.1](https://img.shields.io/badge/Finished%20Checkpoint-1%2E1-success?style=for-the-badge)

1. Let's consider the actual execution of `factorial(3)`. The diagram below depicts how the 
   call stack changes immediately after each invocation and return of the recursive method 
   calls in an execution of `factorial(3)`. Here, we redraw the call stack after each 
   recusive call is added (pushed ↓) and removed (popped ↑) from the call stack during 
   execution. The stack frames include local variables and the return value (using `?` if unknown).

   ![`factorial(3)` pushes](callstack_factorial3_down.png)
   
   ![`factorial(3)` pops](callstack_factorial3_up.png)
   
1. With the above diagram in mind, modify `Fac.java` to  print out the call stack when the
   `factorial` method reaches the base case. Replace the if-statement with the following:
   
   ```java
   if ((n == 0) || (n == 1)) {
       //   i. INSERT ANSWER HERE
       //  ii. INSERT ANSWER HERE
       // iii. INSERT ANSWER HERE
       Thread.currentThread().dumpStack();
       return 1;
   } // if
   ```
   
1. **Next, use Maven to compile and run the code.** Please use the `exec:java` phase to run.
   Once your have observed the program output, please answer the following questions in the
   comments you pasted into your code:
   
   1. Based on the program output, does `dumpStack()` print frames in the order they are
      pushed onto the call stack or in the reverse order? Please write "in order" or "reverse order".
   
   1. There are 8 depictions (i.e., 1 -- 8) of the call stack in the diagrams provided 
      earlier for `factorial(3)`. Which depiction matches up with the program output if
      `dumpStack()` is ignored?
      
   1. In the diagrams provided earlier for `factorial(3)`, we labeled one frame as the
      "calling method". What is the name of the calling method based on the program
      output.
      
1. After you've included your answers in the code, save and commit your changes, 
   **then tag it as `checkpoint-1.2`**.
  
![CP1.2](https://img.shields.io/badge/Finished%20Checkpoint-1%2E2-success?style=for-the-badge)   

1. Make sure you are logged into Nike with X-forwarding enabled. If not, logout and log back in
   appropriately. 
   
1. Run the `CallStackApp` program to explore some call stacks using a GUI: 

   ```
   $ CallStackApp
   ```
   
   ![CallStackApp Screenshot](callstack_app.PNG)
   
1. Add the following multi-line comment to the end of `Fac.java`, then use it to fill in answers
   for the questions below.
   
   ```java
   /* CHECKPOINT 1.3
    *   i. INSERT ANSWER HERE
    *  ii. INSERT ANSWER HERE
    * iii. INSERT ANSWER HERE
    */
   ```
   
   1. Using `CallStackApp`, invoke the `factorial` method with `3` supplied for `n`. Do the call stack
      depcitions in the app line up with the diagram presented for `factorial(3)` earler in this exercise?
      
   2. If you exclude the calling method (which is omitted in the output of `CallStackApp`), what is the
      maximum number of `factorial` frames that need to fit on the call stack at any point in time to
      compute `factorial(9)`? 
      
   3. Using `CallStackApp`, try to invoke the `factorial` method with `10` supplied for `n`. The program
      prevents you from doing that because the author imposed an arbitrary upper limit on the input
      parameter. In your own `Fac.java` file, try different, increasing values for `n` until you find
      one that causes the program to crash when run. When the program crashes it's because the call stack is 
      not big enough to support the maximum number of frames needed to perform the recursion. 
      What is the name of the exception that crashed the program?

1. After you've included your answers in the code, save and commit your changes, 
   **then tag it as `checkpoint-1.3`**.
  
![CP1.3](https://img.shields.io/badge/Finished%20Checkpoint-1%2E3-success?style=for-the-badge)   

1. Create a `cs1302.ce24.Fib` class based on code below that provides a
   recursive [Fibonacci](http://mathworld.wolfram.com/FibonacciNumber.html) method. You may need to add
   a package statement and necessary imports.
   
   ```java
   /**
    * Fibonacci convenience class.
    */
   public class Fib {

       public static void main(String[] args) {
           System.out.println(fibonacci(5));
       } // main

       /**
        * Returns the Fibonacci number at index {@code n}.
        * @param n index
        * @return Fibonacci number at index {@code n}
        */
       public static int fibonacci(int n) {
           if ((n == 0) || (n == 1)) {
               return 1;
           } // if
           return fibonacci(n - 2) + fibonacci(n - 1);
       } // fibonacci
    
   } // Fib
   ```
    
1. **Next, use Maven to compile and run the code.** Please use the `exec:java` phase to run.
   After you've confirmed that it compiles and runs, add and commit your `src` directory which
   now contains `Fib.java` in one of its subdirectories, **then tag it as `checkpoint-2.1`**.
  
![CP2.1](https://img.shields.io/badge/Finished%20Checkpoint-2%2E1-success?style=for-the-badge)

1. The `fibonacci` method that we provided is interesting because each call to `fibonacci` 
   results in it calling itself twice with different parameters. Add the following multi-line 
   comment to the end of `Fib.java`, then use it to fill in answers for the questions below.
   
   ```java
   /* CHECKPOINT 2.1
    *   i. INSERT ANSWER HERE
    *  ii. INSERT ANSWER HERE
    * iii. INSERT ANSWER HERE
    */
    ```
    
    1. Using `CallStackApp`, invoke the `fibonacci` method with `5` supplied for `n`. Scroll
       through the timeline and identify the first frame that is returned to but not immediately
       popped in the next step in the timeline. What is the name of that frame?
       
    1. Another way to visualize recursion is using a digram called a **recursion tree**. Here
       is the recursion tree for `fibonacci(5)`.
   
       ![`fibonacci(5)` recursion tree](callstack_fibonacci5_tree.png)
       
       This recursion tree shows all the frames that execute for `fibonacci(5)`, which may have
       been hard to see if you're only inspecting the call stack itself over time. Using the 
       call stack timeline generated by `CallStackApp` for part (i), traverse the tree. Whenever
       a frame is pushed (↓) onto the call stack, traverse downward toward the frame in the tree;
       likewise, whenever a frame is popped (↑) traverse upward back to its caller. How many times
       do you visit `fibonacci(5)` when performing your traversal (including the initial visit)?
    
    1. ...
    
1. After you've included your answers in the code, save and commit your changes, 
   **then tag it as `checkpoint-2.2`**.

![CP2.2](https://img.shields.io/badge/Finished%20Checkpoint-2%2E2-success?style=for-the-badge)   

1. Another way to visualize recursion is using a digram called a **recursion tree**. Here
   is the recursion tree for `fibonacci(5)`.
   
   ![`fibonacci(5)` recursion tree](callstack_fibonacci5_tree.png)

**CHECKPOINT**

1. Create a new Java file in your Maven project. The FQN for the file should be `cs1302.ce24.RecursionPractice`.
1. Add the class declaration and appropriate package statements at the top of `RecursionPractice.java`.
1. Consider the output below for a call to a method `downUp("Dawgs")`. We will write the code to do this eventually
   but, first, **in your notes**:
   
   * Identify the base case(s). Give an example.
   
   * Identify the recursive case(s).
   
   * Draw the recursion tree for `downUp("Dawgs")`.
   
   ```
   Dawgs
   Dawg
   Daw
   Da
   D
   Da
   Daw
   Dawg
   Dawgs
   ```

**CHECKPOINT**

1. In `RecursionPractice`, create the static method `downUp` that takes a single `String` reference as
   input.
   
1. Execute your code on various input strings to verify that it is working properly.

1. Save and commit your changes.

**CHECKPOINT**

1. Create a new method in `RecursionPractice` called `splitString` with the following signature:

   ```
   public static List<String> splitString(String str, String delim)
   ```
   
   where `List<E>` is [`java.util.List<T>`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html),
   which has known impementations like [`ArrayList<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)
   and [`LinkedList<E>`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html).

1. Implement the `splitString` method using recursion (**no loops!**). The method should split the 
   specified string into tokens based off of the provided delimiter. Each token will be added to
   the returned `List<String>`.
   Here are a few examples:
   
   | Call                                           | Returned List                                 |
   |------------------------------------------------|-----------------------------------------------|
   |`splitString("Hello 1302 students!", " ")`      | `["Hello", "1302", "Students!"]`              |
   |`splitString("1234.1,12345,23213,12,1,1", ",")` | `["1234.1", "12345", "23213", "12", "1", "1"]`|
   |`splitString("GNU's not Unix", "'")`            | `["GNU", "s not Unix"]`                       |
   |`splitString("Recursion is fun!", "9")`         | `["Recursion is fun!"]`                       |
   
1. Execute your code on various input strings to verify that it is working properly.

1. Save and commit your changes.
   
**CHECKPOINT**
<hr/>

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-nc-nd/4.0/)

<small>
Copyright &copy; Michael E. Cotterell, Brad Barnes, and the University of Georgia.
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a> to students and the public.
The content and opinions expressed on this Web page do not necessarily reflect the views of nor are they endorsed by the University of Georgia or the University System of Georgia.
</small>
