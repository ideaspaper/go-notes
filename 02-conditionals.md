# Conditionals

Contents:

- [Conditional operators](#conditional-operators)
- [If/else statement](#ifelse-statement)
- [Short-circuiting](#short-circuiting)
- [If with an initialization statement](#if-with-an-initialization-statement)
- [Switch statement](#switch-statement)
- [Fall-through](#fall-through)
- [Case with multiple values](#case-with-multiple-values)
- [Switch with no expression](#switch-with-no-expression)

## Conditional operators

| Operator |        Description       |
|:--------:|:------------------------:|
|   `==`   | Equal to                 |
|   `!=`   | Not equal to             |
|    `<`   | Less than                |
|   `<=`   | Less than or equal to    |
|    `>`   | Greater than             |
|   `>=`   | Greater than or equal to |

## If/else statement

**main.go**

```go
package main

import "fmt"

func main() {
	age := 12
	if age < 10 {
		fmt.Println("Not old enough")
	} else {
		fmt.Println("Sufficient")
	}
}
```

## Short-circuiting

Go evaluates conditions using a method known as short-circuiting.

**main.go**

```go
package main

import "fmt"

func lessThan10(age int) bool {
	fmt.Println("Checking if age is less than 10")
	return age < 10
}

func lessThan25(age int) bool {
	fmt.Println("Checking if age is less than 25")
	return age < 25
}

func main() {
	age := 5
	if lessThan10(age) || lessThan25(age) {
		fmt.Println("Finished checking")
	}
}
```

In the code above, since `age := 5`, `lessThan10(age)` will evaluates to `true`. Since the comparison logic is `||`, Go will not execute `lessThan25(age)` result.

## If with an initialization statement

**main.go**

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	input := "42"

	// Initialization statement
	// inputInt and err can only be accessed inside if/else statement
	if inputInt, err := strconv.ParseInt(input, 10, 0); err != nil {
		fmt.Println(err)
	} else {
		fmt.Println(inputInt)
	}
}
```

## Switch statement

By default, `switch` in Go will not fall-through. So we do not need to use `break` statement.

**main.go**

```go
package main

import (
	"fmt"
)

func main() {
	input := 1

	switch input {
	case 1:
		fmt.Println("One")
	case 2:
		fmt.Println("Two")
	case 3:
		fmt.Println("Three")
	default:
		fmt.Println("Number is too large")
	}
}
```

## Fall-through

If you need `switch` statement to have fall-through behaviour, you can use `fallthrough` keyword.

**main.go**

```go
package main

import (
	"fmt"
)

func main() {
	input := 1

	switch input {
	case 1:
		fallthrough
	case 2:
		fallthrough
	case 3:
		fmt.Println("Within range")
	default:
		fmt.Println("Number is too large")
	}
}
```

## Case with multiple values

Instead of using the `fallthrough` keyword as example above, you can use the `case` statement to match multiple values as below.

**main.go**

```go
package main

import (
	"fmt"
)

func main() {
	input := 1

	switch input {
	case 1, 2, 3:
		fmt.Println("Within range")
	default:
		fmt.Println("Number is too large")
	}
}
```

## Switch with no expression

**main.go**

```go
package main

import (
	"fmt"
)

func main() {
	input := 1

	switch {
	case input == 1:
		fmt.Println("one")
	case input == 2:
		fmt.Println("two")
	case input == 3:
		fmt.Println("three")
	default:
		fmt.Println("Number is too large")
	}
}
```
