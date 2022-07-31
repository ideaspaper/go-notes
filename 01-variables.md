# Variables

Contents:

- [Declaration](#declaration)
- [Constants](#constants)
- [Strings](#strings)
- [Discovering variable's type](#discovering-variables-type)
- [Converting type](#converting-type)
- [String interpolation](#string-interpolation)

## Declaration

### `:=`

```go
package main

import "fmt"

func main() {
	variable1 := 42 // Type inferred
	variable2 := "fourty-two"
	fmt.Println("variable1:", variable1)
	fmt.Println("variable2:", variable2)

	firstName, middleName, lastName := "Acong", "Suherman", "Sudrajat"
	fmt.Println("name:", firstName, middleName, lastName)

	hobby, maritalStatus, age := "Reading", false, 42
	fmt.Println("hobby:", hobby)
	fmt.Println("maritalStatus:", maritalStatus)
	fmt.Println("age:", age)
}
```

### `var`

`var` can be used outside function.

```go
package main

import "fmt"

var globalVariable = 2

func main() {
	var variable1 = 42 // Type inferred
	var variable2 string = "fourty-two"
	fmt.Println("variable1:", variable1)
	fmt.Println("variable2:", variable2)
	fmt.Println("globalVariable:", globalVariable)

	var (
		variable3 string = "Hello world!"
		variable4 bool   = true
		variable5 int    = 100
	)
	fmt.Println("variable3:", variable3)
	fmt.Println("variable4:", variable4)
	fmt.Println("variable5:", variable5)

	var firstName, middleName, lastName string = "Acong", "Suherman", "Sudrajat"
	fmt.Println("name:", firstName, middleName, lastName)

	var hobby, maritalStatus, age = "Reading", false, 42
	fmt.Println("hobby:", hobby)
	fmt.Println("maritalStatus:", maritalStatus)
	fmt.Println("age:", age)
}
```

## Constants

```go
package main

import "fmt"

func main() {
	const constant = 42 // const can be used anywhere var can
	fmt.Println("constant:", constant)
}
```

## Strings

```go
package main

import (
	"fmt"
	"unicode/utf8"
)

func main() {
	romaji := "wakuwaku"
	hiragana := "わくわく"

	fmt.Println("romaji:", romaji)
	fmt.Println("hiragana:", hiragana)

	fmt.Println("romaji Byte size:", len(romaji))
	fmt.Println("hiragana Byte size:", len(hiragana))

	fmt.Println("number of characters in romaji:", utf8.RuneCountInString(romaji))
	fmt.Println("number of characters in hiragana:", utf8.RuneCountInString(hiragana))
}
```

## Discovering variable's type

```go
package main

import (
	"fmt"
	"reflect"
)

func main() {
	variable1, variable2, variable3 := "fourty two", 42, false
	fmt.Printf("variable1: %T\n", variable1)
	fmt.Printf("variable2: %T\n", variable2)
	fmt.Printf("variable3: %T\n", variable3)

	variable4, variable5, variable6 := "fourty two", 42, false
	fmt.Println("variable4:", reflect.TypeOf(variable4))
	fmt.Println("variable5:", reflect.TypeOf(variable5))
	fmt.Println("variable6:", reflect.TypeOf(variable6))
}
```

## Converting type

### String to numeric and boolean

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	input1 := "42"

	// String to integer
	input1Int, err := strconv.ParseInt(input1, 10, 0) // string, base, bit size
	if err != nil {
		fmt.Println(err)
	} else {
		fmt.Println("input1Int:", input1Int)
		fmt.Printf("Type: %T\n", input1Int)
	}

	// String to float
	input1Float, err := strconv.ParseFloat(input1, 64) // string, bit size
	if err != nil {
		fmt.Println(err)
	} else {
		fmt.Println("input1Int:", input1Float)
		fmt.Printf("Type: %T\n", input1Float)
	}

	// String to boolean
	input2 := "t"
	input2Bool, err := strconv.ParseBool(input2) // string
	if err != nil {
		fmt.Println(err)
	} else {
		fmt.Println("input2Bool:", input2Bool)
		fmt.Printf("Type: %T\n", input2Bool)
	}

	// String to integer
	input3 := "42"
	input3Int, err := strconv.Atoi(input3) // Equivalent to ParseInt(input3, 10, 0)
	if err != nil {
		fmt.Println(err)
	} else {
		fmt.Println("input3Int:", input3Int)
		fmt.Printf("Type: %T\n", input3Int)
	}
}
```

### Integer to string

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	input := 42
	inputString := strconv.Itoa(input)

	fmt.Println("inputString:", inputString)
	fmt.Printf("Type: %T\n", inputString)
}
```

### Numeric to another numeric

```go
package main

import (
	"fmt"
)

func main() {
	input := 42
	inputInt32 := int32(input)
	inputInt64 := int64(input)
	inputFloat32 := float32(input)
	inputFloat64 := float64(input)

	fmt.Println("inputInt32:", inputInt32)
	fmt.Printf("Type: %T\n", inputInt32)
	fmt.Println("inputInt64:", inputInt64)
	fmt.Printf("Type: %T\n", inputInt64)
	fmt.Println("inputFloat32:", inputFloat32)
	fmt.Printf("Type: %T\n", inputFloat32)
	fmt.Println("inputFloat64:", inputFloat64)
	fmt.Printf("Type: %T\n", inputFloat64)
}
```

## String interpolation

```go
package main

import (
	"fmt"
)

func main() {
	name := "Acong"
	age := 42
	result := fmt.Sprintf("Hello my name is %s and I am %d old", name, age)
	fmt.Println(result)
}
```
