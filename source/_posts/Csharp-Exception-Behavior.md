---
title: C# Exception Behavior
date: 2022-06-29 15:04:02
tags:
---

As a programmer, we can see ***a lot of*** *try-catch patterns* in the legacy code.

But sometimes exception messages cannot precisely point out where the error occured.

And this is how C# Exception behaves.

<!-- more -->

## Throw Ex

{% asset_img throw-ex.png throw ex %}

Not Implemented Exception was actually thrown on line 16. But Stack Trace showed the error occured on line 11 instead.

**`throw ex` reset where Exception is raised. Do not use it.**

The following two ways are better choices.

## Throw

{% asset_img throw.png throw %}

Just simplely `throw` can correctly show where the exception occured.

But what if we need custom messages for exceptions?

## Inner Exception

{% asset_img Inner-Exception.png Inner Exception %}

We can package the original exception with a new exception.

The outer exception displayed the message but still contained the original one. So we are able to trace where the error really happened.

## Conlusion

**No Exception Left Behind**

Ignoring or dropping any exception leads more confused debugging.

There are a lot more guidelines for exception handling. But those are other stories.

# Reference

> https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/exceptions/exception-handling
> https://skilltree.my/Events/2022/2/20/Exception-Handling
> https://wiztone.github.io/2019/03/05/CSharp-Exception-YTYKBYD/
