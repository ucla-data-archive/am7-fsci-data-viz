---
layout: reference
permalink: /reference/
---

## Glossary

## Glossary

{:auto_ids}
argument
:   A value given to a function or program when it runs.
    The term is often used interchangeably (and inconsistently) with [parameter](#parameter).

assign
:   To give a value a name by associating a variable with it.

body
:   (of a function): the statements that are executed when a function runs.

comment
:   A remark in a program that is intended to help human readers understand what is going on,
    but is ignored by the computer.
    Comments in Python, R, and the Unix shell start with a `#` character and run to the end of the line;
    comments in SQL start with `--`,
    and other languages have other conventions.

comma-separated values
:   (CSV) A common textual representation for tables
    in which the values in each row are separated by commas.

delimiter
:   A character or characters used to separate individual values,
    such as the commas between columns in a [CSV](#comma-separated-values) file.

documentation
:   Human-language text written to explain what software does,
    how it works, or how to use it.

floating-point number
:   A number containing a fractional part and an exponent.
    See also: [integer](#integer).

for loop
:   A loop that is executed once for each value in some kind of set, list, or range.
    See also: [while loop](#while-loop).

index
:   A subscript that specifies the location of a single value in a collection,
    such as a single pixel in an image.

integer
:   A whole number, such as -12343. See also: [floating-point number](#floating-point-number).

library
:   In R, the directory(ies) where [packages](#package) are stored.

package
:   A collection of R functions, data and compiled code in a well-defined format. Packages are stored in a [library](#library) and loaded using the library() function.

parameter
:   A variable named in the function's declaration that is used to hold a value passed into the call.
    The term is often used interchangeably (and inconsistently) with [argument](#argument).

return statement
:   A statement that causes a function to stop executing and return a value to its caller immediately.

sequence
:   A collection of information that is presented in a specific order.

shape
:   An array's dimensions, represented as a vector.
    For example, a 5×3 array's shape is `(5,3)`.

string
:   Short for "character string",
    a [sequence](#sequence) of zero or more characters.

syntax error
:   A programming error that occurs when statements are in an order or contain characters
    not expected by the programming language.

type
:   The classification of something in a program (for example, the contents of a variable)
    as a kind of number (e.g. [floating-point](#float), [integer](#integer)), [string](#string),
    or something else. In R the command typeof() is used to query a variables type.

while loop
:   A loop that keeps executing as long as some condition is true.
    See also: [for loop](#for-loop).
