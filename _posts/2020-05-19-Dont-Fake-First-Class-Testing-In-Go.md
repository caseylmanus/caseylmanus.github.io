---
layout: post
title:  "Don't fake it; Use first class functions for better Go tests!"
date:   2020-05-19
categories: 
---

# Note: Draft Only!

## First Class Functions
A language supports `first class` functions if a function can be treated identical to any other construct or type in the language.  That is to say, they can be passed as an argument to another function, returned from a function or assigned to a variable. 

#### Function as method parameter

<script src="https://gist.github.com/caseylmanus/bec2cea25bda834c1f224a5694b66c8a.js"></script>

[PlayGround Link](https://play.golang.org/p/IYfliwNQonn)

#### Function as return value

```Go
package main

import "fmt"

func main() {
   do("hello world", getPrinter())
}

func getPrinter() func(s string) {
  return print 
}

func do(s string, printer func(s string)){
  printer(s)
}

func print(s string) {
	fmt.Println(s)
}
```

[PlayGround Link](https://play.golang.org/p/ufF2e1ywjoD)

### Pure functions


## Structs As Dependency Holder vs Data 


## Deconstruct Dependencies
