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
