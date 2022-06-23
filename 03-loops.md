# Loops

Contents:

- [Looping](#looping)
- [Looping with range](#looping-with-range)
- [Labels](#labels)
- [Using labels with loop](#using-labels-with-loop)

## Looping

```go
package main

import (
	"fmt"
)

func main() {
	// Initialization i := 0
	// Condition      i < 5
	// Post           i++
	for i := 0; i < 5; i++ {
		fmt.Println("i:", i)
	}

	// Equivalent form of while
	i := 0
	for i < 5 {
		fmt.Println("i:", i)
		i++
	}

	// Infinite loop
	for {
		var input string
		fmt.Print("Enter \"q\" to quit: ")
		fmt.Scanln(&input)
		if input == "q" {
			break
		}
	}
}
```

## Looping with range

```go
package main

import (
	"fmt"
)

func main() {
	romaji := "Hello world!"

	for i, v := range romaji {
		fmt.Println(i, ":", v)
	}

	for i, v := range romaji {
		fmt.Printf("%d : %c\n", i, v)
	}

	hiragana := "ありがとう"

	for i, v := range hiragana {
		// i will represents Byte location
		fmt.Printf("%d : %c\n", i, v)
	}

	array := [3]string{"Acong", "Suherman", "Sudrajat"}
	for i, v := range array {
		// i will represents array's index
		fmt.Println(i, ":", v)
	}
}
```

## Labels

```go
package main

import (
	"fmt"
)

func main() {
	i := 0

Label:
	fmt.Println(i)
	i++
	if i < 5 {
		goto Label
	}
}
```

## Using labels with loop

```go
package main

import (
	"fmt"
)

func main() {
Outerloop:
	for i := 0; i < 3; i++ {
		for j := 0; j < 3; j++ {
			fmt.Printf("i: %d | j: %d\n", i, j)
			if j == 2 {
				break Outerloop
			}
		}
	}
}

// i: 0 | j: 0
// i: 0 | j: 1
// i: 0 | j: 2
```
