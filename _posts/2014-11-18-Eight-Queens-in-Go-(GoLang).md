---
layout: post
title:  "8 Queens Puzzle in Go (GoLang)"
date:   2014-11-18 09:19:46
categories: golang EightQueensPuzzle
---

I am currently in the process of evaluating [GO](http://golang.org).  One of the excersizes I always do when looking at a new language is to implement the 8 queens puzzle, which is an old computational exercise to determine how many different combinations of 8 queens can be placed on a Chess board (which is 8 x 8 squares) in positions which they cannot attach each other.  

In computer science this problem is most often implemented as nQueens, meaning n Queens on an n x n board.  To read more about the problem see [here](http://en.wikipedia.org/wiki/Eight_queens_puzzle).

Implementing this in GO was extremely easy, and fast.  I didn't do any performance calculations, but compared to previous interations I've done in C++, C#, Java, and others this version seems to perform the best.  You can run an example on the [Go Playground](http://play.golang.org/p/PmjJRUh-Ks)


Here is the source code on GitHub: 

<script src="https://gist.github.com/caseylmanus/df10ad3457b916c32373.js"></script>