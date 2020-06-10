---
layout: post
title:  "Don't fake it; Use first class functions for better Go tests!"
date:   2020-05-19
categories: 
---

# Note: Draft Only!

## TLDR; 
Mocking or faking interfaces comes with significant overhead, and unit testing using a mock framework usually does more to exercise the mock than the target code. The use of first class functions to encasulate dependency can greatly increase testability. 

## All about the func 
### First Class Functions
A language supports `first class` functions if a function can be treated identical to any other construct or type in the language.  That is to say, they can be passed as an argument to another function, returned from a function or assigned to a variable. 

#### Function as method parameter
```
package main

import "fmt"

type printer func(string)

func main() {
   do("hello world", print)
}

func do(s string, p printer){
  p(s)
}

func print(s string) {
	fmt.Println(s)
}
```


#### Function as return value

```
package main 

import "fmt"

type printer func(string)

func main() {
   do("hello world", getPrinter())
}

func getPrinter() printer {
  return func(s string) {
    fmt.Println(s)
  } 
}

func do(s string, p printer){
  printer(s)
}
```

#### Functions as variables
```
package main 

import (
  "fmt"
  "strings"
)

type printer func(string)

func main() {
   var p printer = print
   do("hello world", p)
}

func do(s string, p printer) {
   p(s)
}

func print(s string){
  fmt.Println(s)
}
```

### Pure functions
A function can be described a `pure` when:
 - Given the same input, will always return the same output.
 - Produces no side effects.

#### Pure function
```
package main

func main() {
   if add(1,2) != 3 {
       panic("the world is ending")
   }
} 

func add(a, b int) int {
  return a + b
}
```
this `add` function can make promises that given the same set of inputs, it will always return the same output, and it makes promises that it does not have side effects.  It modifies nothing external to itself and it's output.

#### Testability
A pure function has the highest possible level of testability
```
func Test_add(t *testing.T){
  assert.True(t, 3, add(1, 2))
  assert.True(t, 4, add(2, 2))
  //...more edge cases if they exist
}
```

**Assumption:** a method will no return value can never be considered a pure function. In Go, I'd extend that assumption to say in most cases a function that only returns an error, however there are obvious exceptions such as functions intended as assertions only.

####  Not Pure function
```
type Person struct {
  First, Last string 
}

func makeFirstNameRight(p &Person){
  p.First = "Casey" // only valid first name 
}
```
making that a pure function is still possible; however you need consider the trade-offs for performance to gain this increased testability 
```
func makeFirstNameRight(p Person) Person {
  p.First = "Casey"
  return p
}
```

### Closures

## Structs, gotta have'm

### Structs As Data Holder 

### Structs As Dependency Holder 

### Deconstruct Dependencies


## Interfaces, sure but don't abuse

### Alternative to mock libraries/frameworks