#Basic Operators
#基本操作

An operator is a special symbol or phrase that you use to check, change, or combine values. For example, the addition operator (+) adds two numbers together (as in let i = 1 + 2). More complex examples include the logical AND operator && (as in if enteredDoorCode && passedRetinaScan) and the increment operator ++i, which is a shortcut to increase the value of i by 1.

运算符是一个特殊的符号，或者你用它来检查，更改或合并值。例如，加法运算符（+），将两个数字相加（如令i=1+2）。更复杂的例子包括逻辑AND运算符&&（如 if enteredDoorCode&& passedRetinaScan）和递增运算符++我，这是由1增加i的值的快捷方式。

Swift supports most standard C operators and improves several capabilities to eliminate common coding errors. The assignment operator (=) does not return a value, to prevent it from being mistakenly used when the equal to operator (==) is intended. Arithmetic operators (+, -, *, /, % and so forth) detect and disallow value overflow, to avoid unexpected results when working with numbers that become larger or smaller than the allowed value range of the type that stores them. You can opt in to value overflow behavior by using Swift’s overflow operators, as described in Overflow Operators.

Swift支持大部分标准C运算twfy，并改善一些功能，以消除常见的编码错误。赋值运算符（=）没有返回值，以防止它被误用时，等于运算符（==）拟。算术运算符（+， - ，*，/，％等）检测并禁止值溢出，与变得比存储他们的类型所允许的值的范围更大或更小数目的工作时，以避免意外的结果。您可以选择价值溢出行为使用斯威夫特的溢出运营商，如溢出运营商介绍。

Unlike C, Swift lets you perform remainder (%) calculations on floating-point numbers. Swift also provides two range operators (a..<b and a...b) not found in C, as a shortcut for expressing a range of values.

This chapter describes the common operators in Swift. Advanced Operators covers Swift’s advanced operators, and describes how to define your own custom operators and implement the standard operators for your own custom types.

Terminology

Operators are unary, binary, or ternary:

Unary operators operate on a single target (such as -a). Unary prefix operators appear immediately before their target (such as !b), and unary postfix operators appear immediately after their target (such as i++).

Binary operators operate on two targets (such as 2 + 3) and are infix because they appear in between their two targets.

Ternary operators operate on three targets. Like C, Swift has only one ternary operator, the ternary conditional operator (a ? b : c).

The values that operators affect are operands. In the expression 1 + 2, the + symbol is a binary operator and its two operands are the values 1 and 2.

Assignment Operator

The assignment operator (a = b) initializes or updates the value of a with the value of b:

If the right side of the assignment is a tuple with multiple values, its elements can be decomposed into multiple constants or variables at once:

Unlike the assignment operator in C and Objective-C, the assignment operator in Swift does not itself return a value. The following statement is not valid:

This feature prevents the assignment operator (=) from being used by accident when the equal to operator (==) is actually intended. By making if x = y invalid, Swift helps you to avoid these kinds of errors in your code.

Arithmetic Operators

Swift supports the four standard arithmetic operators for all number types:

Addition (+)

Subtraction (-)

Multiplication (*)

Division (/)

Unlike the arithmetic operators in C and Objective-C, the Swift arithmetic operators do not allow values to overflow by default. You can opt in to value overflow behavior by using Swift’s overflow operators (such as a &+ b). See Overflow Operators.

The addition operator is also supported for String concatenation:

Two Character values, or one Character value and one String value, can be added together to make a new String value:

See also Concatenating Strings and Characters.

Remainder Operator

The remainder operator (a % b) works out how many multiples of b will fit inside a and returns the value that is left over (known as the remainder).

Note

The remainder operator (%) is also known as a modulo operator in other languages. However, its behavior in Swift for negative numbers means that it is, strictly speaking, a remainder rather than a modulo operation.

Here’s how the remainder operator works. To calculate 9 % 4, you first work out how many 4s will fit inside 9:

 image: ../Art/remainderInteger_2x.png
You can fit two 4s inside 9, and the remainder is 1 (shown in orange).

In Swift, this would be written as:

To determine the answer for a % b, the % operator calculates the following equation and returns remainder as its output:

a = (b × some multiplier) + remainder

where some multiplier is the largest number of multiples of b that will fit inside a.

Inserting 9 and 4 into this equation yields:

9 = (4 × 2) + 1

The same method is applied when calculating the remainder for a negative value of a:

Inserting -9 and 4 into the equation yields:

-9 = (4 × -2) + -1

giving a remainder value of -1.

The sign of b is ignored for negative values of b. This means that a % b and a % -b always give the same answer.

Floating-Point Remainder Calculations

Unlike the remainder operator in C and Objective-C, Swift’s remainder operator can also operate on floating-point numbers:

In this example, 8 divided by 2.5 equals 3, with a remainder of 0.5, so the remainder operator returns a Double value of 0.5.

 image: ../Art/remainderFloat_2x.png
Increment and Decrement Operators

Like C, Swift provides an increment operator (++) and a decrement operator (--) as a shortcut to increase or decrease the value of a numeric variable by 1. You can use these operators with variables of any integer or floating-point type.

Each time you call ++i, the value of i is increased by 1. Essentially, ++i is shorthand for saying i = i + 1. Likewise, --i can be used as shorthand for i = i - 1.

The ++ and -- symbols can be used as prefix operators or as postfix operators. ++i and i++ are both valid ways to increase the value of i by 1. Similarly, --i and i-- are both valid ways to decrease the value of i by 1.

Note that these operators modify i and also return a value. If you only want to increment or decrement the value stored in i, you can ignore the returned value. However, if you do use the returned value, it will be different based on whether you used the prefix or postfix version of the operator, according to the following rules:

If the operator is written before the variable, it increments the variable before returning its value.

If the operator is written after the variable, it increments the variable after returning its value.

For example:

In the example above, let b = ++a increments a before returning its value. This is why both a and b are equal to to the new value of 1.

However, let c = a++ increments a after returning its value. This means that c gets the old value of 1, and a is then updated to equal 2.

Unless you need the specific behavior of i++, it is recommended that you use ++i and --i in all cases, because they have the typical expected behavior of modifying i and returning the result.

Unary Minus Operator

The sign of a numeric value can be toggled using a prefixed -, known as the unary minus operator:

The unary minus operator (-) is prepended directly before the value it operates on, without any white space.

Unary Plus Operator

The unary plus operator (+) simply returns the value it operates on, without any change:

Although the unary plus operator doesn’t actually do anything, you can use it to provide symmetry in your code for positive numbers when also using the unary minus operator for negative numbers.

Compound Assignment Operators

Like C, Swift provides compound assignment operators that combine assignment (=) with another operation. One example is the addition assignment operator (+=):

The expression a += 2 is shorthand for a = a + 2. Effectively, the addition and the assignment are combined into one operator that performs both tasks at the same time.

Note

The compound assignment operators do not return a value. You cannot write let b = a += 2, for example. This behavior is different from the increment and decrement operators mentioned above.

A complete list of compound assignment operators can be found in Expressions.

Comparison Operators

Swift supports all standard C comparison operators:

Equal to (a == b)

Not equal to (a != b)

Greater than (a > b)

Less than (a < b)

Greater than or equal to (a >= b)

Less than or equal to (a <= b)

Note

Swift also provides two identity operators (=== and !==), which you use to test whether two object references both refer to the same object instance. For more information, see Classes and Structures.

Each of the comparison operators returns a Bool value to indicate whether or not the statement is true:

Comparison operators are often used in conditional statements, such as the if statement:

For more on the if statement, see Control Flow.

Ternary Conditional Operator

The ternary conditional operator is a special operator with three parts, which takes the form question ? answer1 : answer2. It is a shortcut for evaluating one of two expressions based on whether question is true or false. If question is true, it evaluates answer1 and returns its value; otherwise, it evaluates answer2 and returns its value.

The ternary conditional operator is shorthand for the code below:

Here’s an example, which calculates the height for a table row. The row height should be 50 points taller than the content height if the row has a header, and 20 points taller if the row doesn’t have a header:

The preceding example is shorthand for the code below:

The first example’s use of the ternary conditional operator means that rowHeight can be set to the correct value on a single line of code. This is more concise than the second example, and removes the need for rowHeight to be a variable, because its value does not need to be modified within an if statement.

The ternary conditional operator provides an efficient shorthand for deciding which of two expressions to consider. Use the ternary conditional operator with care, however. Its conciseness can lead to hard-to-read code if overused. Avoid combining multiple instances of the ternary conditional operator into one compound statement.

Nil Coalescing Operator

The nil coalescing operator (a ?? b) unwraps an optional a if it contains a value, or returns a default value b if a is nil. The expression a is always of an optional type. The expression b must match the type that is stored inside a.

The nil coalescing operator is shorthand for the code below:

The code above uses the ternary conditional operator and forced unwrapping (a!) to access the value wrapped inside a when a is not nil, and to return b otherwise. The nil coalescing operator provides a more elegant way to encapsulate this conditional checking and unwrapping in a concise and readable form.

Note

If the value of a is non-nil, the value of b is not evaluated. This is known as short-circuit evaluation.

The example below uses the nil coalescing operator to choose between a default color name and an optional user-defined color name:

The userDefinedColorName variable is defined as an optional String, with a default value of nil. Because userDefinedColorName is of an optional type, you can use the nil coalescing operator to consider its value. In the example above, the operator is used to determine an initial value for a String variable called colorNameToUse. Because userDefinedColorName is nil, the expression userDefinedColorName ?? defaultColorName returns the value of defaultColorName, or "red".

If you assign a non-nil value to userDefinedColorName and perform the nil coalescing operator check again, the value wrapped inside userDefinedColorName is used instead of the default:

Range Operators

Swift includes two range operators, which are shortcuts for expressing a range of values.

Closed Range Operator

The closed range operator (a...b) defines a range that runs from a to b, and includes the values a and b. The value of a must not be greater than b.

The closed range operator is useful when iterating over a range in which you want all of the values to be used, such as with a for-in loop:

For more on for-in loops, see Control Flow.

Half-Open Range Operator

The half-open range operator (a..<b) defines a range that runs from a to b, but does not include b. It is said to be half-open because it contains its first value, but not its final value. As with the closed range operator, the value of a must not be greater than b.

Half-open ranges are particularly useful when you work with zero-based lists such as arrays, where it is useful to count up to (but not including) the length of the list:

Note that the array contains four items, but 0..<count only counts as far as 3 (the index of the last item in the array), because it is a half-open range. For more on arrays, see Arrays.

Logical Operators

Logical operators modify or combine the Boolean logic values true and false. Swift supports the three standard logical operators found in C-based languages:

Logical NOT (!a)

Logical AND (a && b)

Logical OR (a || b)

Logical NOT Operator

The logical NOT operator (!a) inverts a Boolean value so that true becomes false, and false becomes true.

The logical NOT operator is a prefix operator, and appears immediately before the value it operates on, without any white space. It can be read as “not a”, as seen in the following example:

The phrase if !allowedEntry can be read as “if not allowed entry.” The subsequent line is only executed if “not allowed entry” is true; that is, if allowedEntry is false.

As in this example, careful choice of Boolean constant and variable names can help to keep code readable and concise, while avoiding double negatives or confusing logic statements.

Logical AND Operator

The logical AND operator (a && b) creates logical expressions where both values must be true for the overall expression to also be true.

If either value is false, the overall expression will also be false. In fact, if the first value is false, the second value won’t even be evaluated, because it can’t possibly make the overall expression equate to true. This is known as short-circuit evaluation.

This example considers two Bool values and only allows access if both values are true:

Logical OR Operator

The logical OR operator (a || b) is an infix operator made from two adjacent pipe characters. You use it to create logical expressions in which only one of the two values has to be true for the overall expression to be true.

Like the Logical AND operator above, the Logical OR operator uses short-circuit evaluation to consider its expressions. If the left side of a Logical OR expression is true, the right side is not evaluated, because it cannot change the outcome of the overall expression.

In the example below, the first Bool value (hasDoorKey) is false, but the second value (knowsOverridePassword) is true. Because one value is true, the overall expression also evaluates to true, and access is allowed:

Combining Logical Operators

You can combine multiple logical operators to create longer compound expressions:

This example uses multiple && and || operators to create a longer compound expression. However, the && and || operators still operate on only two values, so this is actually three smaller expressions chained together. The example can be read as:

If we’ve entered the correct door code and passed the retina scan, or if we have a valid door key, or if we know the emergency override password, then allow access.

Based on the values of enteredDoorCode, passedRetinaScan, and hasDoorKey, the first two mini-expressions are false. However, the emergency override password is known, so the overall compound expression still evaluates to true.

Explicit Parentheses

It is sometimes useful to include parentheses when they are not strictly needed, to make the intention of a complex expression easier to read. In the door access example above, it is useful to add parentheses around the first part of the compound expression to make its intent explicit:

The parentheses make it clear that the first two values are considered as part of a separate possible state in the overall logic. The output of the compound expression doesn’t change, but the overall intention is clearer to the reader. Readability is always preferred over brevity; use parentheses where they help to make your intentions clear.

The Basics

Strings and Characters

Copyright © 2014 Apple Inc. All rights reserved. Terms of Use | Privacy Policy | Updated: 2014-09-17