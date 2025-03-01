Download link :https://programming.engineering/product/cs536-p5-programming-assignment-5-solution-wumbo-type-checker-implementation-testing/

# CS536-P5-Programming-Assignment-5-Solution-Wumbo-Type-Checker-Implementation-Testing
CS536 P5 Programming Assignment 5 Solution – Wumbo Type Checker Implementation &amp; Testing
For this assignment you will write a type checker for Wumbo programs represented as abstract-syntax trees. Your main task will be to write type checking methods for the nodes of the AST. In addition you will need to:

Modify P5.java.

Write two test inputs: typeErrors.wumbo and test.wumbo to test your new code.

Getting Started

Download zip file

Start the project by downloading p5.zip

The files:

ast.java



Wumbo.cup



Wumbo.jlex



DuplicateSymException.java



EmpytSymTableException.java



ErrMsg.java



Sym.java



SymTable.java



Type.java



Makefile



P5.java



typeErrors.wumbo



test.wumbo



Specifications

Type Checking



Preventing Cascading Errors



Other Tasks



P5.java



Writing test Inputs



Some Advice



Type Checking

The type checker will determine the type of every expression represented in the abstract-syntax tree and will use that information to identify type errors. In the Wumbo language we have the following types:

int, bool, void (as function return types only), struct types, and function types.

CS536 P5 2020/4/11, 21:00

CS536 P5 2020/4/11, 21:00

CS536 P5 2020/4/11, 21:00

CS536 P5 2020/4/11, 21:00

Preventing Cascading Errors

A single type error in an expression or statement should not trigger multiple error messages. For example, assume that P is the name of a struct type, p is a variable declared to be of struct type P, and f is a function that has one integer parameter and returns a bool. Each of the following should cause only one error message:

cout <<

P + 1

// P + 1 is

an error; the

write is OK

(true +

3)

* 4

// true +

3

is an error; the * is OK

true &&

(false || 3) // false ||

3 is an error; the && is OK

f(“a” *

4);

// “a” * 4 is an error; the call is OK

1 + p();

3)

== x

// p() is

an error; the +

is OK

(true +

// true +

3

is an error; the == is OK

// regardless of the type

of x

One way to accomplish this is to use a special ErrorType for expressions that contain type errors. In the second example above, the type given to (true + 3) should be ErrorType, and the type-check method for the multiplication node should not report “Arithmetic operator applied to non-numeric operand” for the first

operand. But note that the following should each cause two error messages (assuming the same declarations of f as above):

true +

“hello”

// one error

for each of the non-int

operands of the

+

1

+ f(true)

// one for the bad arg type

and one for the

2nd

operand of the +

1

+ f(1, 2)

// one for

the

wrong number

of args and one

for

the 2nd operand of the +

return

3+true;

// in a void

function: one error for

the 2nd operand

to +

// and one

for

returning a value

To provide some help with this issue, here is an example input file , along with the corresponding error messages. (Note: This is not meant to be a complete test of the type checker; it is provided merely to help you understand some of the messages you need to report, and to help you find small typos in your error messages. If you run your program on the example file and put the output into a new file, you can use the Linux utility diff to compare your file of error messages with the one supplied here. This will help both to make sure that your code finds the errors it is supposed to find, and to uncover small typos you may have made in the error messages.)

Other Tasks

P5.java

You will need to modify P5.java.

The main program, P5.java, will be similar to P4.java, except that if it calls the name analyzer and there are no errors, it will then call the type checker.

Writing Test Inputs

You will need to write two input files to test your code:

typeErrors.wumbo should contain code with errors detected by the type checker. For every type error listed in the table above, you should include an instance of that error for each of the relevant operators, and in each part of a program where the error can occur (e.g., in a top-level statement, in a statement inside a while loop, etc).

test.wumbo should contain code with no errors that exercises all of the type-check methods that you wrote for the different AST nodes. This means that it should include (good) examples of every kind of statement and expression.

Note that your typeErrors.wumbo should cause error messages to be output, so to know whether your type

CS536 P5 2020/4/11, 21:00

CS536 P5 2020/4/11, 21:00

http://pages.cs.wisc.edu/~loris/cs536/asn/p5/p5.html Page 7 of 7
