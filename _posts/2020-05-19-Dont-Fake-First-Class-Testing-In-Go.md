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

### Pure functions
A function can be described a `pure` when:
 - Given the same input, will always return the same output.
 - Produces no side effects.

## Structs As Dependency Holder vs Data 


## Deconstruct Dependencies
