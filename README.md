# cs1302-ce24

> "To understand recursion, you must understand recursion"

This class exercise explores the concept of [recursion](https://github.com/cs1302uga/cs1302-ce24).

## References and Prerequisites

* [`CSCI 1302 Recursion Tutorial`](https://github.com/cs1302uga/cs1302-tutorials/blob/master/recursion.md)

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
      
   1. Update the POM so that the project works with Java 8. After that, use Git to track the `pom.xml`, 
      then commit it to the repository, then add and commit the `pom.xml` file to the repository.
   
   1. Delete the Maven-generated driver (i.e., `src/main/java/cs1302/ce24/App.java`) and the unit test files 
      (i.e., everything under `src/test/java`). Finally, add and commit the `src` directory to the repository.
   
## Exercise Steps

1. Create a `cs1302.ce24.Fib` class based on code below that provides a
   recursive [Fibonacci](http://mathworld.wolfram.com/FibonacciNumber.html) method.

   ```java
    public class Fib {

        public static void main(String[] args) {
            System.out.println(fibonacci(5));
        } // main

        public static int fibonacci(int n) {
            if(n == 0) return 1;
            if(n == 1) return 1;
            return fibonacci(n - 2) + fibonacci(n - 1);      
        } // fibonacci
        
    } // Fib
    ```
    
1. **Next, use Maven to compile and the code.** Please use the `exec:java` phase to run.
   After you've confirmed that it compiles and runs, please add and commit `Fib.java`.

1. The diagram below depicts how the call stack changes immediately after each invocation
   and return of the recursive method calls in an execution of `fibonacci(2)`. Here, we 
   redraw the call stack after each recusive call is added (pushed) and removed (popped) from
   the call stack during execution. The stack frames include local variables and the return 
   value (using `?` if unknown). 

    ```
     immediately             immediately             immediately             immediately
     after calling           after calling           after returning         after calling 
     fibonacci(2)            fibonacci(0)            fibonacci(0)            fibonacci(1)
    |------------------|    |------------------|    |------------------|    |------------------|
    | [calling method] | => | [calling method] | => | [calling method] | => | [calling method] | =>
    |------------------|    |------------------|    |------------------|    |------------------|   
    | [fibonacci(2)]   |    | [fibonacci(2)]   |    | [fibonacci(2)]   |    | [fibonacci(2)]   |   
    | n = 2            |    | n = 2            |    | n = 2            |    | n = 2            |   
    | return ? +       |    | return ? + ?     |    | return 1 + ?     |    | return 1 + ?     |   
    |------------------|    |------------------|    |------------------|    |------------------|   
                            | [fibonacci(0)]   |                            | [fibonacci(1)]   |  
                            | return  1        |                            | return 1         |  
                            |------------------|                            |------------------|  
    ```
    ```
     immediately             immediately        
     after returning         after returning
     fibonacci(1)            fibonacci(2)       
    |------------------|    |------------------|
    | [calling method] | => | [calling method] |
    |------------------|    |------------------|
    | [fibonacci(2)]   |     Now has value 2
    | n = 2            |    
    | return 1 + 1     |    
    |------------------|    
                            
    ```
    For larger inputs, redrawing the call stack whenever a frame is added or removed becomes time consuming
    and error-prone. An alternative is to only redraw the call stack when a frame is removed (popped). In other
    words, we add frames to the existing picture and redraw only when a method returns. The example below 
    demonstrates this approach. 
    
    ```
     immediately             immediately             immediately             immediately
     after calling           after returning         fter returning          after returning
     fibonacci(2)            fibonacci(0)            fibonacci(1)            fibonacci(2)
     and fibonacci(0)        and calling 
                             fibonacci(1)
    |------------------|    |------------------|    |------------------|    |------------------|
    | [calling method] | => | [calling method] | => | [calling method] | => | [calling method] |
    |------------------|    |------------------|    |------------------|    |------------------|   
    | [fibonacci(2)]   |    | [fibonacci(2)]   |    | [fibonacci(2)]   |     Now has value 2
    | n = 2            |    | n = 2            |    | n = 2            | 
    | return ? +       |    | return ? + ?     |    | return 1 + 1     | 
    |------------------|    |------------------|    |------------------| 
    | [fibonacci(0)]   |    | [fibonacci(1)]   |  
    | return  1        |    | return 1         |  
    |------------------|    |------------------|  
    ```

   Using the second approach, diagram the changes to the call stack as `fibonacci(4)` executes. 
   
**CHECKPOINT**

1. Create a new Java file in your Maven project. The FQN for the file should be `cs1302.ce24.RecursionPractice`.
1. Add the class declaration and appropriate package statements at the top of `RecursionPractice.java`.
1. In `RecursionPractice`, create a static method called `downUp` that takes a single `String` reference as
   input. If `downUp("Dawgs")` is invoked, then the following output should be produced:
   
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

1. Execute your code on various input strings to verify that it is working properly.
1. Save and commit your changes.

**CHECKPOINT**

1. Create a new method in `RecursionPractice` called `splitString` with the following signature:
   `public static List<String> splitString(String str, String delim)`.

1. Implement the `splitString` method using recursion (no loops!). The method should split the 
   specified string into tokens based off of the provided delimiter. Each token will be added to
   the returned `List<String>`.
   Here are a few examples:
   
   |Call                                          |Returned List                                |
   |----------------------------------------------|---------------------------------------------|
   |splitString("Hello 1302 students!", " ")      | ["Hello", "1302", "Students!"]              |
   |splitString("1234.1,12345,23213,12,1,1", ",") | ["1234.1", "12345", "23213", "12", "1", "1"]|
   |splitString("GNU's not Unix", "'")            | ["GNU", "s not Unix"]                       |
   |splitString("Recursion is fun!, "9")          | ["Recursion is fun!"]                       |
   
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
