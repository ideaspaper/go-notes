# Functions

Contents:

- [Creating a function](#creating-a-function)
- [Parameters and arguments](#parameters-and-arguments)
- [Passing by pointer](#passing-by-pointer)
- [Return values](#return-values)
- [Variadic functions](#variadic-functions)
- [Anonymous functions](#anonymous-functions)
- [Closure](#closure)

## Creating a function

```go
package main

import (
	"fmt"
)

func greet() {
	fmt.Println("おはようございます。") // Good morning
}

func main() {
	greet()
}
```

## Parameters and arguments

```go
package main

import (
	"fmt"
)

// add has 3 parameters:
//   - a      : int
//   - b      : int
//   - message: string
func add(a, b int, message string) {
	result := a + b
	fmt.Printf("%s: %d\n", message, result)
}

func main() {
	// Calling add with 3 arguments
	add(4, 2, "The result is")
}
```

## Passing by pointer

a.k.a. **pass by reference**.

```go
package main

import (
	"fmt"
)

func swap(a, b *int) {
	*a, *b = *b, *a
}

func addDesu(input *string) {
	*input = *input + "です" // desu
}

func main() {
	a, b := 4, 2
	fmt.Println("Before:", a, b)
	swap(&a, &b)
	fmt.Println("After:", a, b)

	input := "わくわく" // wakuwaku
	fmt.Println("Before:", input)
	addDesu(&input)
	fmt.Println("After:", input)
}
```

## Return values

```go
package main

import (
	"errors"
	"fmt"
	"strconv"
)

func add(a, b int) int {
	result := a + b
	return result
}

// Named return values
func multiply(a, b int) (result int) {
	result = a * b
	// Naked return
	// Automatically returns the current value of named return values
	// Caution: use this only on short functions
	return
}

func countOddEven(input string) (int, int, error) {
	odd, even := 0, 0
	for _, v := range input {
		intV, err := strconv.Atoi(string(v))
		if err != nil {
			return 0, 0, errors.New("invalid input")
		}
		if intV%2 != 0 {
			odd++
		} else {
			even++
		}
	}
	return odd, even, nil
}

func main() {
	input1, input2 := 4, 2
	fmt.Println("add:", add(input1, input2))

	input3, input4 := 2, 4
	fmt.Println("multiply:", multiply(input3, input4))

	input5 := "12345"
	if odd, even, err := countOddEven(input5); err != nil {
		fmt.Println("countOddEven", err)
	} else {
		fmt.Println("countOddEven:", odd, even)
	}
}
```

## Variadic functions

Variadic functions are functions that can be called with any number of trailing arguments.

```go
package main

import (
	"errors"
	"fmt"
	"strconv"
)

func printMessagesXTimes(times int, messages ...string) {
	for i := 0; i < times; i++ {
		fmt.Println("Time:", i)
		for _, message := range messages {
			fmt.Println(message)
		}
	}
}

func main() {
	printMessagesXTimes(2, "Acong", "Suherman", "Sudrajat")
}
```

## Anonymous functions

```go
package main

import (
	"fmt"
)

func executeAFunction(function func()) {
	function()
}

func main() {
	executeAFunction(func() {
		fmt.Println("This is from an anonymous function")
	})
}
```

## Closure

```go
package main

import (
	"fmt"
)

func main() {
	tempFunction := closureDemo()
	fmt.Println(tempFunction()) // 1
	fmt.Println(tempFunction()) // 2
	fmt.Println(tempFunction()) // 3
	fmt.Println(tempFunction()) // 4
}
```
