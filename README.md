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

1. Use Git to clone the repository for this exercise onto Nike into a subdirectory called `cs1302-ce24`:

   ```
   $ git clone --depth 1 https://github.com/cs1302uga/cs1302-ce24.git
   ```

1. Change into the `cs1302-ce24` directory that was just created and look around. There should be
   almost nothing there! That's okay.

    **We might not give you any starter code.  Not sure yet.**
   
## Exercise Steps

1. Consider the recursive [Fibonacci](http://mathworld.wolfram.com/FibonacciNumber.html) program given below.

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

1. Draw a diagram that illustrates a new stack frame being added to the call stack or an existing stack frame
   being removed (popped) from the call stack as `fibonacci(4)` is executed. Be sure to include any local variables
   and return values in each stack frame.
    
   Redraw the entire picture after each modification to the stack frame as is done in the tutorial.
   The picture below illustrates the execution of `fibonacci(2)`. Use this as an example for your diagram.
   
   Example:
    ```
     immediately             immediately             immediately             immediately
     after calling           after calling           after returning         after calling 
     fibonacci(2)            fibonacci(1)            fibonacci(1)            fibonacci(0)
    |------------------|    |------------------|    |------------------|    |------------------|
    | [calling method] | => | [calling method] | => | [calling method] | => | [calling method] | =>
    |------------------|    |------------------|    |------------------|    |------------------|   
    | [fibonacci(2)]   |    | [fibonacci(2)]   |    | [fibonacci(2)]   |    | [fibonacci(2)]   |   
    | n = 2            |    | n = 2            |    | n = 2            |    | n = 2            |   
    | return ?         |    | return ?         |    | return 1 + ?     |    | return 1 + ?     |   
    |------------------|    |------------------|    |------------------|    |------------------|   
                            | [fibonacci(1)]   |                            | [fibonacci(0)]   |  
                            | return  1        |                            | return 0         |  
                            |------------------|                            |------------------|  

     immediately             immediately        
     after returning         after returning
     fibonacci(0)            fibonacci(2)       
    |------------------|    |------------------|
    | [calling method] | => | [calling method] |
    |------------------|    |------------------|
    | [fibonacci(2)]   |     Now has value 6
    | n = 2            |    
    | return 1 + 0     |    
    |------------------|    
                            
    ```

**CHECKPOINT**
   
1. In your notes, write your expected output for the four `System.out.println` statements in the code based 
   on the diagram you created in the previous step. 
   
1. Make sure you are in the `cs1302-ce11` directory. Write the exact command to:
   1. Compile `Driver.java` specifying `bin` as the default package location for your compiled code.
   1. Run `cs1302.list.Driver`.
   
   **NOTE:** This program depends on two different sets of compiled code: i) the compiled code you placed
   into `bin`; and ii) the compiled code in the JAR file. You will need to place the paths to the default 
   package locations for both on the class path in order to run your program.

1. Write the output from the program in your notes. If your expected output does not match the output from the 
   program execution, repeat the last three steps using a new piece of paper.
   
**CHECKPOINT**

1. In `Driver.java`, add a method to print the string value of the third `StringList.Node` in the list. Your
   method should take a single `StringList.Node` parameter representing the starting node. The method must
   begin with the starting node and traverse the `next` links to print the third node.
   
1. In your notes, write down the expected output of calling your new method from `main` passing in 
   the preexisting `StringList.Node` references (`end`, `node`, and `n`) as the actual parameters.

1. From the `main` method of `Driver.java`, make three separate calls to your new method using `end`, `node`,
   and `n` as the actual parameters.
   
1. Compile and run your `Driver` program. 

1. Write the output from the program in your notes. If your expected output does not match the output from the 
   program execution, indicate the reason(s) in your notes.
   
1. Your `Driver` program likely threw an unchecked exception when you ran it. Update your code to handle this 
   type of error instead of crashing. In your notes, explain how you handled it and why you handled it this way.

**CHECKPOINT**

1. In `Driver.java`, add a method to insert a `StringList.Node` into the third position in the list. It should 
   shift the node currently at that position (if any) and any subsequent nodes to the right. Your 
   method should take two `StringList.Node` parameters, one representing the starting node and another
   representing a node to insert. The method must begin with the starting node and traverse the `next` links to
   move toward the correct position. You should assume the node to insert is not already in the list.
  
1. In your notes, draw the expected linked list after calling your new insert method from `main` passing in 
   the `node` reference as the starting point along with a new node containing the string "Cupid". Your diagram 
   should illustrate any nodes that have been created along with their associated string values and next 
   references.

1. At the end of the `main` method of `Driver.java`, add the method call described in the previous step.
   
1. Write a method to verify that your insert method worked correctly. The output from this method should convince
   your instructor/TA that your method worked.

**CHECKPOINT**

<hr/>

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-nc-nd/4.0/)

<small>
Copyright &copy; Michael E. Cotterell, Brad Barnes, and the University of Georgia.
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a> to students and the public.
The content and opinions expressed on this Web page do not necessarily reflect the views of nor are they endorsed by the University of Georgia or the University System of Georgia.
</small>
