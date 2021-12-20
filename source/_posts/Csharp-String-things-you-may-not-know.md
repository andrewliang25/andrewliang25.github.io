---
title: C# String - things you may not know
date: 2021-12-10 23:17:43
tags:
---


We use `string` very often in programming. `"A" + "B"`, such things like this.
But have you ever think about that is `string` maybe not value type?

<!-- more -->

## Value Type or Reference Type?

Let us see an example:
```
int intA = 1;
int intB = intA;
Console.WriteLine(int.ReferenceEquals(intA, intA)); // False
Console.WriteLine(int.ReferenceEquals(intA, intB)); // False
```
`int` is clearly value type, they are being boxed when you call object.ReferenceEquals.
Each integer is boxed inside an object instance.
Thus, this is actually comparing references between two boxed values, which clearly aren't equal.
And how about `string`?
```
string strA = "aa";
string strB = strA;
Console.WriteLine(string.ReferenceEquals(strA, strA)); // True
Console.WriteLine(string.ReferenceEquals(strA, strB)); // True
```
We can see that `strA` and `strB` share same reference.
Now you may be considering `string` as some sort of `char[]`.
But in reality, modifying `strA` does not affect `strB`, right?


## Mutable or Immutable?

Lets see another example:
```
string strA = "AA";
string strB = strA;
Console.WriteLine(strA); // AA
Console.WriteLine(strB); // AA
Console.WriteLine(string.ReferenceEquals(strA, strB)); //True

strA += "BB";
Console.WriteLine(strA); // AABB
Console.WriteLine(strB); // AA
Console.WriteLine(string.ReferenceEquals(strA, strB)); //False
```
`char[]` is mutable, which means the value can be modified after assignment.
Instead, `string` is immutable, you cannot change the value since it was been initialized.
So what `strA += "BB"` actually does is creating a new string object `"AABB"` re-assigned to strA.


## String Pool

`string` is very commonly used in C# programming, there is a mechanism called string pool.
Which collects new created string instances for reusing to minimize memory allocations.
```
string strA = "AA";
string strB = "AA";
Console.WriteLine(string.ReferenceEquals(strA, strB)); //True
```
`strB` points to the same `"AA"` instance as `strA`, since `"AA"` has been created and collected in string pool.



# Reference

> https://github.com/microsoft/referencesource/blob/master/mscorlib/system/string.cs
> https://docs.microsoft.com/en-us/windows/communitytoolkit/high-performance/stringpool
> https://wiztone.github.io/2019/02/18/string-YTYKBYD/