# Arrays and slices

Contents:

- [Declaring an array](#declaring-an-array)
- [Declaring a slice](#declaring-a-slice)
- [Append and exceeding capacity](#append-and-exceeding-capacity)
- [Copy, insert and remove](#copy-insert-and-remove)
- [Common use of `cap()`](#common-use-of-cap)

## Declaring an array

```go
package main

import (
	"fmt"
)

func main() {
	var input1 [3]int
	var input2 [3]string
	fmt.Println("input1:", input1)
	fmt.Println("input2:", input2)

	input3 := [3]int{42, 43, 44}
	input4 := [3]string{"fourty-two", "fourty-three", "fourty-four"}
	fmt.Println("input3:", input3)
	fmt.Println("input4:", input4)
	fmt.Println("input4[0]:", input4[0])

	input5 := [...]int{1, 2, 3, 4, 5}
	fmt.Println("input5:", input5)
	fmt.Println("input5 length:", len(input5))

	// 2D array
	input6 := [3][3]int{{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}
	fmt.Println("input6:")
	for _, v := range input6 {
		for _, w := range v {
			fmt.Print(w)
		}
		fmt.Println()
	}
}
```

## Declaring a slice

Slice is a dynamically-sized, flexible view into the elements of an array. A slice has 3 properties as below:

- `ptr`: a pointer to the underlying array
- `len`: length of the slice
- `cap`: capacity of the slice

```go
package main

import (
	"fmt"
)

func main() {
	// Creating an empty slice
	var slice1 = make([]int, 5)
	fmt.Println("slice1:", slice1)
	fmt.Println("length:", len(slice1))
	fmt.Println("capacity:", cap(slice1))
	var slice2 = make([]int, 5, 10)
	fmt.Println("slice2:", slice2)
	fmt.Println("length:", len(slice2))
	fmt.Println("capacity:", cap(slice2))

	// Declaring a slice with initial value
	slice3 := []string{"Acong", "Suherman", "Sudrajat"}
	fmt.Println("slice3:", slice3)
	fmt.Println("length:", len(slice3))
	fmt.Println("capacity:", cap(slice3))

	// Creating slice from an array
	primes := [6]int{2, 3, 5, 7, 11, 13}
	slice4 := primes[1:4]
	fmt.Println("slice4:", slice4)
	fmt.Println("length:", len(slice4))
	fmt.Println("capacity:", cap(slice4))

	// Converting array to slice
	names := [3]string{"Acong", "Suherman", "Sudrajat"}
	slice5 := names[:]
	fmt.Println("slice5:", slice5)
	fmt.Println("length:", len(slice5))
	fmt.Println("capacity:", cap(slice5))
}
```

## Append and exceeding capacity

Since slices' size is dynamic, we can add more values to it by using `append`. But when an `append` operation result exceeds the capacity of the slice, a new underlying array will be created.

```go
package main

import (
	"fmt"
)

func main() {
	primes := [3]int{42, 43, 44}
	slice1 := primes[:]
	slice2 := primes[:]
	fmt.Println("slice1 (initial):", slice1, "=> cap:", cap(slice1))
	fmt.Println("slice2 (initial):", slice2, "=> cap:", cap(slice2))

	slice1[0] = 10
	fmt.Println("slice1 (after 0th element changed):", slice1, "=> cap:", cap(slice1))
	fmt.Println("slice2 (after 0th element changed):", slice2, "=> cap:", cap(slice2))

	slice1 = append(slice1, 45, 46, 47)
	slice1[0] = 11
	fmt.Println("slice1 (after append & 0th element changed):", slice1, "=> cap:", cap(slice1))
	fmt.Println("slice2 (after append & 0th element changed):", slice2, "=> cap:", cap(slice2))
}
```

## Copy, insert and remove

```go
package main

import (
	"fmt"
)

func main() {
	// Copying an array
	array1 := [3]int{1, 2, 3}
	array2 := array1
	array2[0] = 10
	fmt.Println("array1:", array1)
	fmt.Println("array2:", array2)

	// Copying a slice
	slice1 := []int{1, 2, 3}
	slice2 := make([]int, len(slice1))
	copy(slice2, slice1)
	slice2[0] = 10
	fmt.Println("slice1:", slice1)
	fmt.Println("slice2:", slice2)

	// Inserting a value to slice
	slice3 := []int{1, 2, 3, 4, 5, 6}
	insertIndex := 3
	insertValue := 42
	insertResult := append(slice3[:insertIndex+1], slice3[insertIndex:]...)
	// [1 2 3 4 4 5 6]
	insertResult[insertIndex] = insertValue
	fmt.Println("insertResult:", insertResult)
	// [1 2 3 42 4 5 6]

	// Removing a value from slice
	slice4 := []int{1, 2, 3, 4, 5, 6}
	removeIndex := 3
	removeResult := append(slice4[:removeIndex], slice4[removeIndex+1:]...)
	fmt.Println("removeResult:", removeResult)
	// [1 2 3 5 6]
}
```

## Common use of `cap()`

```go
package main

import "fmt"

func main() {
	a := make([]int, 5)
	fmt.Println(a) // [0 0 0 0 0]
	for i := range a {
		a[i] = i
	}
	fmt.Println(a) // [0 1 2 3 4]
}
```

In this example, we used `make()` to create a slice and had it pre-allocate 5 elements. We then used the `cap()` function in the loop to iterate through each zeroed element, filling each until it reached the pre-allocated capacity. While we can achive the same result using `append()`, using `cap()` will avoid any additional memory allocations that would have been needed using the `append()` function.
