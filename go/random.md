# reslice
[link](https://stackoverflow.com/questions/27938177/golang-slice-slicing-a-slice-with-sliceabc)

The syntax has been introduced in Go 1.2, as I mentioned in "Re-slicing slices in Golang".
It is documented in Full slice expressions:

a[low : high : max]
constructs a slice of the same type, and with the same length and elements as the simple slice expression a[low : high].
Additionally, it controls the resulting slice's capacity by setting it to max - low.
Only the first index may be omitted; it defaults to 0.

After slicing the array a:
```
a := [5]int{1, 2, 3, 4, 5}
t := a[1:3:5]
```
the slice t has type []int, length 2, capacity 4, and elements
```
t[0] == 2
t[1] == 3
```

# Errors in Go 1.13 The Unwrap method
[link](https://go.dev/blog/go1.13-errors)

Go 1.13 introduces new features to the errors and fmt standard library packages to simplify working with errors that contain other errors. The most significant of these is a convention rather than a change: an error which contains another may implement an Unwrap method returning the underlying error. If e1.Unwrap() returns e2, then we say that e1 wraps e2, and that you can unwrap e1 to get e2.

Following this convention, we can give the QueryError type above an Unwrap method that returns its contained error:
```
func (e *QueryError) Unwrap() error { return e.Err }
```
The result of unwrapping an error may itself have an Unwrap method; we call the sequence of errors produced by repeated unwrapping the error chain.

#### Examining errors with Is and As
The Go 1.13 errors package includes two new functions for examining errors: Is and As.

The errors.Is function compares an error to a value.
```
// Similar to:
//   if err == ErrNotFound { … }
if errors.Is(err, ErrNotFound) {
    // something wasn't found
}
```
The As function tests whether an error is a specific type.
```
// Similar to:
//   if e, ok := err.(*QueryError); ok { … }
var e *QueryError
// Note: *QueryError is the type of the error.
if errors.As(err, &e) {
    // err is a *QueryError, and e is set to the error's value
}
```

In the simplest case, the errors.Is function behaves like a comparison to a sentinel error, and the errors.As function behaves like a type assertion. When operating on wrapped errors, however, these functions consider all the errors in a chain.

#### Wrapping errors with %w
As mentioned earlier, it is common to use the fmt.Errorf function to add additional information to an error.
```
if err != nil {
    return fmt.Errorf("decompress %v: %v", name, err)
}
```

# defer
The behavior of defer statements is straightforward and predictable. There are three simple rules:

1. A deferred function’s arguments are evaluated when the defer statement is evaluated.
2. Deferred function calls are executed in Last In First Out order after the surrounding function returns.
3. Deferred functions may read and assign to the returning function’s named return values.

# flag package
Package flag implements command-line flag parsing.

#### Usage
Define flags using flag.String, Bool, Int, etc.

This declares an integer flag, -n, stored in the pointer nFlag, with type *int:
```
import "flag"
var nFlag = flag.Int("n", 1234, "help message for flag n")
```

After all flags are defined, call
```
flag.Parse()
```
#### Command line flag syntax 
The following forms are permitted:
```
-flag
--flag   // double dashes are also permitted
-flag=x
-flag x  // non-boolean flags only
```
