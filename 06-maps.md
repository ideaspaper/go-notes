# Maps

Contents:
- [Declaring a map](#declaring-a-map)
- [Deleting an element](#deleting-an-element)

## Declaring a map

```go
package main

import "fmt"

func main() {
	m1 := make(map[string]string)
	m1["firstName"] = "Acong"
	m1["lastName"] = "Suherman"
	fmt.Println(m1["firstName"])
	fmt.Println(m1["lastName"])

	m2 := map[string]string{"firstName": "Djoko", "lastName": "Susanto"}
	fmt.Println(m2["firstName"])
	fmt.Println(m2["lastName"])
}
```

## Deleting an element

```go
package main

import "fmt"

func main() {
	m := map[string]string{"firstName": "Djoko", "lastName": "Susanto"}
	fmt.Println(m)
	delete(m, "lastName")
	fmt.Println(m)
}
```
