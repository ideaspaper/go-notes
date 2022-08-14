# Structs

Contents:

- [Declaring a struct](#declaring-a-struct)

## Declaring a struct

```go
package main

import "fmt"

type Person struct {
	FirstName string
	LastName string
	Age int 
}

func main() {
	person1 := Person{"Acong", "Suherman", 17}
	fmt.Println(person1)
	person2 := &Person{"Djoko", "Susanto", 18}
	fmt.Println(person2)
	person3 := Person{LastName: "Hermanto", Age: 19, FirstName: "Sitorus"}
	fmt.Println(person3)
}
```
