---
layout: post
title:  "Don't fake it; Use first class functions for better Go tests!"
date:   2020-05-19
categories: 
---

# Note: Draft Only!

## TLDR; 
Mocking or faking interfaces comes with significant overhead, and unit testing using a mock framework usually does more to exercise the mock than the target code. The use of first class functions to encasulate dependency can greatly increase testability. 

## First Class Functions
A language supports `first class` functions if a function can be treated identical to any other construct or type in the language.  That is to say, they can be passed as an argument to another function, returned from a function or assigned to a variable. 

#### Function as method parameter
In the code below, a function is passed to the `do` method.  The `do` method needs only to know that it accepts a 
function with signature `func(string)` and doesn't need to care what the function does.  

<script src="https://gist.github.com/caseylmanus/bec2cea25bda834c1f224a5694b66c8a.js"></script>

[PlayGround Link](https://play.golang.org/p/IYfliwNQonn)

#### Functions can be declared as types
The same code as above, but we've assigned the print function a named type, previously it was anonymous.

<script src="https://gist.github.com/caseylmanus/6a8ece93f2010490ca97eed8c7e781f2.js"></script>

[PlayGround Link](https://play.golang.org/p/-cFkW0knnps)

#### Function as return value

```
package main 

import "fmt"

func main() {
   do("hello world", getPrinter())
}

func getPrinter() func(s string) {
  return func(s string) {
    fmt.Println(s)
  } 
}

func do(s string, printer func(s string)){
  printer(s)
}
```

[PlayGround Link](https://play.golang.org/p/ufF2e1ywjoD)

### Pure functions


## Structs As Dependency Holder vs Data 


## Deconstruct Dependencies
