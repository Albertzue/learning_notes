
Ch1 Go Tooling
---
compiler (go build) \
code formatter (go fmt)\
dependency manager (go mod)\
test runner (go test)\
a tool that scans for common coding mistakes (go vet)

Ch2 The Predeclared Types
---
**The Zero Value**\
Go, like most modern languages, assigns a default zero value to any variable that is declared but not assigned a value 

0b for binary (base 2), 0o for octal (base 8), or 0x for hexadecimal (base 16). You can use either upper- or lowercase letters for the prefix. A leading 0 with no letter after it is another way to represent an octal literal. Do not use it, as it is very confusing 

You could put an underscore between every digit in your literal (1_2_3_4), but don’t. Use them to improve readability by breaking up base 10 numbers at the thousands place or to break up binary, octal, or hexadecimal numbers at 1-, 2-, or 4-byte boundaries.

These are delimited with backquotes (`) and can contain any character except a backquote

**Complex types (you’re probably not going to use these)

ch2 A Taste of Strings and Runes
---
Strings in Go are immutable; you can reassign the value of a string variable, but you cannot change the value of the string that is assigned to it.

The rune type is an alias for the int32 type, just as byte is an alias for uint8.

ch2 Explicit Type Conversion
---
Go doesn’t allow automatic type promotion between variables. You must use a type conversion when variable types do not match. Even different-sized integers and floats must be converted to the same type to interact. 

In fact, no other type can be converted to a bool, implicitly or explicitly. If you want to convert from another data type to boolean, you must use one of the comparison operators (==, !=, >, <, <=, or >=). For example, to check if variable x is equal to 0, the code would be x == 0. If you want to check if string s is empty, use s == "".

ch2 var Versus :=
---
There’s one more way to use var. If you are declaring multiple variables at once, you can wrap them in a declaration list:
```
var (
    x    int
    y        = 20
    z    int = 30
    d, e     = 40, "hello"
    f, g string
)
```

The := operator can do one trick that you cannot do with var: it allows you to assign values to existing variables too. As long as at least one new variable is on the lefthand side of the :=, any of the other variables can already exist:
```
x := 10
x, y := 30, "hello"
```

Using := has one limitation. If you are declaring a variable at the package level, you must use var because := is not legal outside of functions.
