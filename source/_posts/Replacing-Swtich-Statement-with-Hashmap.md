---
title: Replacing Swtich Statement with Hashmap
date: 2022-11-25 16:54:05
tags:
---


{% asset_img Reverse-Polish-Notation.jpg Reverse Polish Notation %}

## Reverse Polish Notation

Reverse Polish Notation (RPN) also called postfix notation.\
Which which operators follow their operands and does not need any parentheses.\
For example, `3 * (10 + 5)` in RPN is `3 10 5 + *` as above.

How do we write an evaluate function?

<!-- more -->

## Switch Statement

Assume that all inputs are valid, we do not need to consider edge cases.\
The easiest way to implement is by using stack.\
Iterate through input array, push operands into stack, pop operands out and calculate if operator occurs.\
For four operators `+`, `-`, `*`, `/`, obviously we can use `if else` statement or better, `switch` statement, to determine the operation.

Let us seen the code using switch statement below:
```go
// Go
func evalRPN(tokens []string) int {
	stack := []int{}
	for _, token := range tokens {
		// if token is an operator, calculate
		// if not, push number into stack
		if token == "+" || token == "-" || token == "*" || token == "/" {
			// pop last two elements
			a, b := stack[len(stack)-2], stack[len(stack)-1]
			// determine operation and push result
			switch token {
			case "+":
				stack = append(stack[:len(stack)-2], a+b)
			case "-":
				stack = append(stack[:len(stack)-2], a-b)
			case "*":
				stack = append(stack[:len(stack)-2], a*b)
			case "/":
				stack = append(stack[:len(stack)-2], a/b)
			}
		} else {
			num, _ := strconv.Atoi(token) // convert string into int
			stack = append(stack, num)
		}
	}
	return stack[0]
}
```

## Hashmap

Seems a bit annoying since it does very similar things in 4 cases.\
We can take all 4 operators and operations out into a hashmap.\
By accessing hashmap with operator, we can get the operation that correspond to it.

Here is the code example below:

```go
// Go
func evalRPN(tokens []string) int {
	stack := []int{}
	operators := map[string]func(int, int) int{
		"+": func(a, b int) int { return a + b },
		"-": func(a, b int) int { return a - b },
		"*": func(a, b int) int { return a * b },
		"/": func(a, b int) int { return a / b },
	}

	for _, token := range tokens {
		if calculate, exist := operators[token]; exist {
			a, b := stack[len(stack)-2], stack[len(stack)-1]
			stack = append(stack[:len(stack)-2], calculate(a, b))
		} else {
			num, _ := strconv.Atoi(token)
			stack = append(stack, num)
		}
	}
	return stack[0]
}
```

It seems more ordered than before, right?

## Conclusion

Replacing switch statement with hashmap increase tidiness and readability of code.

Note: I have never mentioned there is any performance improvement.

Actually in most cases, replacing `switch` with hashmap does not increase performance, maybe even a little bit worse.

Since compilers and interpreters are fully optimized for `switch`. `switch` will be turned into mapping table, same as hashmap. Sometimes `if else` if too many cases.

In this particular situation, hashmap may have better performance while consuming more memory.
But it is more about readibility.

*It may decrease readibility for some unskilled programmers. They can only understand fully flattened code with single-dimension.*

If there are all professional programmer in your team, try it.

{% asset_img Joma-Tech-Hashmap.jpg Joma Tech %}

> Reference
> https://leetcode.com/problems/evaluate-reverse-polish-notation/
> https://commons.wikimedia.org/wiki/File:Reverse_Polish_Notation_Stack_Example.jpg
> https://youtu.be/5bId3N7QZec