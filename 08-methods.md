# Methods

Contents:

- [Methods on struct](#methods-on-struct)
- [Pointer receiver](#pointer-receiver)
- [Method on custom type](#method-on-custom-type)

## Methods on struct

A method is a function with a special **receiver** argument. The **receiver** appears in its own argument list between the `func` keyword and the method name.

```go
package main

import "fmt"

type Person struct {
	FirstName string
	LastName string
	Age int 
}

func (p Person) Greet() {
	fmt.Printf("Hello my name is %s %s, I am %d years old\n", p.FirstName, p.LastName, p.Age)
}

func (p Person) GoodBye() {
	fmt.Println("Bye bye")
}

func main() {
	person := &Person{"Acong", "Suherman", 17}
	person.Greet()
	person.GoodBye()
}
```

## Pointer receiver

Methods with pointer receivers can modify the value to which the receiver points. Since methods often need to modify their receiver, pointer receivers are more common than value receivers.

```go
package main

import "fmt"

type Person struct {
	FirstName string
	LastName string
	Age int 
}

func (p *Person) Greet() {
	fmt.Printf("Hello my name is %s %s, I am %d years old\n", p.FirstName, p.LastName, p.Age)
}

func (p *Person) GoodBye() {
	fmt.Println("Bye bye")
}

func (p *Person) Birthday() {
	fmt.Printf("It's %s birthday!\n", p.FirstName)
	p.Age++
}

func main() {
	person := &Person{"Acong", "Suherman", 17}
	person.Greet()
	person.GoodBye()
	person.Birthday()
	person.Greet()
}
```

## Method on custom type

```go
package main

import "fmt"

type Day int;

func (d Day) Name() string {
	daysName := map[int]string{
		1: "Monday",
		2: "Tuesday",
		3: "Wednesday",
		4: "Thursday",
		5: "Friday",
		6: "Saturday",
		7: "Sunday",
	}
	result, ok := daysName[int(d)]
	if !ok {
		return "wrong input"
	}
	return result
}

func main() {
	day := Day(1)
	fmt.Println(day.Name())
}
```
