
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

ch2 Using const
---
Go doesn’t provide a way to specify that a value calculated at runtime is immutable. For example, the following code will fail to compile with the error x + y (value of type int) is not constant:
```
x := 5
y := 10
const z = x + y // this won't compile!
```

 there are no immutable arrays, slices, maps, or structs, and there’s no way to declare that a field in a struct is immutable

ch3 Arrays—Too Rigid to Use Directly
---
```
var x = [...]int{1, 2, 3}
var y = [3]int{1, 2, 3}
fmt.Println(x == y) // prints true
```

A slice is the first type you’ve seen that isn’t comparable. It is a compile-time error to use == to see if two slices are identical or != to see if they are different. The only thing you can compare a slice with using == is nil

Since Go 1.21, the slices package in the standard library includes two functions to compare slices. The slices.Equal function takes in two slices and returns true if the slices are the same length, and all of the elements are equal. It requires the elements of the slice to be comparable. The other function, slices.EqualFunc, lets you pass in a function to determine equality and does not require the slice elements to be comparable

```
x := []int{1, 2, 3, 4, 5}
y := []int{1, 2, 3, 4, 5}
z := []int{1, 2, 3, 4, 5, 6}
s := []string{"a", "b", "c"}
fmt.Println(slices.Equal(x, y)) // prints true
fmt.Println(slices.Equal(x, z)) // prints false
fmt.Println(slices.Equal(x, s)) // does not compile
```



One slice is appended onto another by using the ... operator to expand the source slice into individual values (you’ll learn more about the ... operator in “Variadic Input Parameters and Slices”):
```
y := []int{20, 30, 40}
x = append(x, y...)
```

ch3 Capacity
---
Every slice also has a capacity, which is the number of consecutive memory locations reserved. This can be larger than the length.

If you try to add additional values when the length equals the capacity, the append function uses the Go runtime to allocate a new backing array for the slice with a larger capacity. The values in the original backing array are copied to the new one, the new values are added to the end of the new backing array, and the slice is updated to refer to the new backing array.
```
x := make([]int, 5, 10)
```
This creates an int slice with a length of 5 and a capacity of 10.

Go 1.21 added a clear function that takes in a slice and sets all of the slice’s elements to their zero value. The length of the slice remains unchanged.
```
x := []string{"a", "b", "c", "d"}
y := x[:2]
z := x[1:]
d := x[1:3]
e := x[:]
fmt.Println("x:", x)
fmt.Println("y:", y)
fmt.Println("z:", z)
fmt.Println("d:", d)
fmt.Println("e:", e)

x: [a b c d]
y: [a b]
z: [b c d]
d: [b c]
e: [a b c d]
```

When you take a slice from a slice, you are not making a copy of the data. Instead, you now have two variables that are sharing memory. This means that changes to an element in a slice affect all slices that share that element.

If you need to create a slice that’s independent of the original, use the built-in copy function


ch3 Converting Arrays to Slices
---
Slices aren’t the only thing you can slice. If you have an array, you can take a slice from it using a slice expression. This is a useful way to bridge an array to a function that takes only slices. To convert an entire array into a slice, use the [:] syntax:
```
xArray := [4]int{5, 6, 7, 8}
xSlice := xArray[:]
```

Be aware that taking a slice from an array has the same memory-sharing properties as taking a slice from a slice.

When you convert a slice to an array, the data in the slice is copied to new memory. That means that changes to the slice won’t affect the array, and vice versa.

The following code:
```
xSlice := []int{1, 2, 3, 4}
xArray := [4]int(xSlice)
smallArray := [2]int(xSlice)
xSlice[0] = 10
fmt.Println(xSlice)
fmt.Println(xArray)
fmt.Println(smallArray)
```
While the size of the array can be smaller than the size of the slice, it cannot be bigger.

ch3 Maps
---
Maps are like slices in several ways:
<ol>
<li>Maps automatically grow as you add key-value pairs to them.</li>
<li>If you know how many key-value pairs you plan to insert into a map, you can use make to create a map with a specific initial size.</li>
<li>Passing a map to the len function tells you the number of key-value pairs in a map.</li>
<li>The zero value for a map is nil.</li>
<li>Maps are not comparable. You can check if they are equal to nil, but you cannot check if two maps have identical keys and values using == or differ using !=.</li>
</ol>

 Go provides the comma ok idiom to tell the difference between a key that’s associated with a zero value and a key that’s not in the map:
```
m := map[string]int{
    "hello": 5,
    "world": 0,
}
v, ok := m["hello"]
fmt.Println(v, ok)

v, ok = m["world"]
fmt.Println(v, ok)

v, ok = m["goodbye"]
fmt.Println(v, ok)
```
```
m := map[string]int{
    "hello": 5,
    "world": 10,
}
delete(m, "hello")
```
The delete function takes a map and a key and then removes the key-value pair with the specified key. If the key isn’t present in the map or if the map is nil, nothing happens. The delete function doesn’t return a value.

The clear function that you saw in “Emptying a Slice” works on maps also. A cleared map has its length set to zero, unlike a cleared slice.

Two functions in the package are useful for comparing if two maps are equal, maps.Equal and maps.EqualFunc. They are analogous to the slices.Equal and slices.EqualFunc

ch3 Anonymous Structs
---
You can also declare that a variable implements a struct type without first giving the struct type a name. This is called an anonymous struct:
```
var person struct {
    name string
    age  int
    pet  string
}

person.name = "bob"
person.age = 50
person.pet = "dog"

pet := struct {
    name string
    kind string
}{
    name: "Fido",
    kind: "dog",
}
```

Just as Go doesn’t allow comparisons between variables of different primitive types, Go doesn’t allow comparisons between variables that represent structs of different types. Go does allow you to perform a type conversion from one struct type to another if the fields of both structs have the same names, order, and types. Let’s see what this means.

ch4
---
A shadowing variable is a variable that has the same name as a variable in a containing block. For as long as the shadowing variable exists, you cannot access a shadowed variable

ch4 label for
---
```
func main() {
    samples := []string{"hello", "apple_π!"}
outer:
    for _, sample := range samples {
        for i, r := range sample {
            fmt.Println(i, r, string(r))
            if r == 'l' {
                continue outer
            }
        }
        fmt.Println()
    }
}
```

For the sake of completeness, Go does include a fallthrough keyword, which lets one case continue on to the next one


ch5 Variadic Input Parameters and Slices
---
```
func addTo(base int, vals ...int) []int {
    out := make([]int, 0, len(vals))
    for _, v := range vals {
        out = append(out, base+v)
    }
    return out
}
```
Multiple Return Values
The first difference that you’ll see between Go and other languages is that Go allows for multiple return values. Let’s add a small feature to the previous division program. You’re going to return both the dividend and the remainder from the function. Here’s the updated function:
```
func divAndRemainder(num, denom int) (int, int, error) {
    if denom == 0 {
        return 0, 0, errors.New("cannot divide by zero")
    }
    return num / denom, num % denom, nil
}
```
Use _ whenever you don’t need to read a value that’s returned by a function.

ch5 Named Return Values
---
```
func divAndRemainder(num, denom int) (result int, remainder int, err error) {
    if denom == 0 {
        err = errors.New("cannot divide by zero")
        return result, remainder, err
    }
    result, remainder = num/denom, num%denom
    return result, remainder, err
}
```
If you want to name only some of the return values, you can do so by using _ as the name for any return values you want to remain nameless.

Blank Returns—Never Use These!
If you use named return values, you need to be aware of one severe misfeature in Go: blank (sometimes called naked) returns. If you have named return values, you can just write return without specifying the values that are returned. This returns the last values assigned to the named return values

ch6 
---
 if a nil pointer is passed into a function via a parameter or a field on a parameter, you cannot set the value within the function

within the Go runtime, a map is implemented as a pointer to a struct. Passing a map to a function means that you are copying a pointer

When a slice is copied to a different variable or passed to a function, a copy is made of the length, capacity,
Meanwhile, passing a slice to a function has more complicated behavior: any modification to the slice’s contents is reflected in the original variable, but using append to change the length isn’t reflected in the original variable, even if the slice has a capacity greater than its length
The result is that a slice that’s passed to a function can have its contents modified, but the slice can’t be resized. As the only usable linear data structure, slices are frequently passed around in Go programs

The first is the GOGC environment variable. The garbage collector looks at the heap size at the end of a garbage-collection cycle and uses the formula CURRENT_HEAP_SIZE + CURRENT_HEAP_SIZE*GOGC/100 to calculate the heap size that needs to be reached to trigger the next garbage-collection cycle.

Setting GOGC to off disables garbage collection. This will make your programs run faster. However, turning off garbage collection on a long-running process will potentially use all available memory on your computer. This is not usually considered optimal behavior.

The value for GOMEMLIMIT is specified in bytes, but you can optionally use the suffixes B, KiB, MiB, GiB, and TiB. For example, GOMEMLIMIT=3GiB sets the memory limit to 3 gibibytes

ch7
---

In addition to struct literals, you can use any primitive type or compound type literal to define a concrete type. Here are a few examples:
```
type Score int
type Converter func(string)Score
type TeamScores map[string]Score
```

There is one key difference between declaring methods and functions: methods can be defined only at the package block level, while functions can be defined inside any block.

One thing you might notice is that you were able to call the pointer receiver method even though c is a value type. When you use a pointer receiver with a local variable that’s a value type, Go automatically takes the address of the local variable when calling the method. In this case, c.Increment() is converted to (&c).Increment().

hey can be pointer receivers (the type is a pointer) or value receivers (the type is a value type). The following rules help you determine when to use each kind of receiver:

If your method modifies the receiver, you must use a pointer receiver.

If your method needs to handle nil instances (see “Code Your Methods for nil Instances”), then it must use a pointer receiver.

If your method doesn’t modify the receiver, you can use a value receiver.




```
const (
    Uncategorized MailCategory = iota
    Personal
    Spam
    Social
    Advertisements
)
```
The first constant in the const block has the type specified, and its value is set to iota. Every subsequent line has neither the type nor a value assigned to it. When the Go compiler sees this, it repeats the type and the assignment to all the subsequent constants in the block, which is iota
```
const (
    Field1 = 0
    Field2 = 1 + iota
    Field3 = 20
    Field4
    Field5 = iota
)

func main() {
    fmt.Println(Field1, Field2, Field3, Field4, Field5)
}
```
```
0 2 20 20 4
```

ch10
---
The **go get** command downloads modules and updates the go.mod file. You have two options when using go get. The simplest option is to tell go get to scan your module’s source code and add any modules that are found in import statements to go.mod

As I mentioned, there’s another way to use go get. Instead of telling it to scan your source code to discover modules, you can pass the module paths to go get


Sharp-eyed readers might have noticed that when we used go get a second time, the go: downloading messages weren’t displayed. The reason is that Go maintains a module cache on your local computer. Once a version of a module is downloaded, a copy is kept in the cache. Source code is pretty compact, and drives are pretty large, so this isn’t usually a concern. However, if you want to delete the module cache, use the command go clean -modcache.

Use iota for “internal” purposes only.

**If you want to fix this label automatically, use the command go mod tidy. It scans your source code and synchronizes the go.mod and go.sum files with your module’s source code, adding and removing module references. It also makes sure that the indirect comments are correct.**


First, you can see what versions of the module are available with the go list command:

```
$ go list -m -versions github.com/learning-go-book-2e/simpletax
github.com/learning-go-book-2e/simpletax v1.0.0 v1.1.0
```

go mod graph shows the dependency graph of your module and all its dependencies.

**go get -u**\
The -u flag instructs get to update modules providing dependencies
of packages named on the command line to use newer minor or patch
releases when available.


It’s enabled by running the command go mod vendor. This creates a directory called vendor at the top level of your module that contains all your module’s dependencies. These dependencies are used in place of the module cache stored on your computer.

A replace directive redirects all references to a module across all your module’s dependencies and replaces them with the specified fork of the module. It looks like this:
```
replace github.com/jonbodner/proteus => github.com/someone/my_proteus v1.0.0
```

The right side must have a version specified, but specifying a version is optional for the left side. If a version is specified on the left side, only that specific version will be replaced. If the version is not specified, any version of the original module will be replaced with the specific version of the fork.

A replace directive can also refer to a path on your local filesystem:
```
replace github.com/jonbodner/proteus => ../projects/proteus
```

Go provides the exclude directive to prevent a specific version of a module from being used:
```
exclude github.com/jonbodner/proteus v0.10.1
```
This is done by adding a retract directive to the go.mod file of your module. It consists of the word retract and the semantic version that should no longer be used. If a range of versions shouldn’t be used, you can exclude all versions in that range by placing the upper and lower bounds within brackets, separated by a comma. While it’s not required, you should include a comment after a version or version range to explain the reason for the retraction.

You can validate that your code is working with the public module by setting the environment variable GOWORK=off and building your application:
```
$ rm workspace_app
$ GOWORK=off go build
$ ./workspace_app
```
