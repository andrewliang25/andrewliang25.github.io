---
title: Browser Force https
date: 2021-09-13 11:51:10
tags:
---

## Prologue

As a web developer, it is common to use localhost to preview the blog.
But still something weird came up: browser forcing the path go https.
This article just record how to get rid of it.
<!-- more -->


## The Problem

After entering `http://localhost:4000/`, browser automatically using https, which looks like `https://localhost:4000/`. And show error code: `ERR_SSL_PROTOCOL_ERROR`.

The situation mainly cause from HTTP Strict Transport Security. If you ever visited a website through https, the browser will remember it. And next time you visit the same domain, browser automatically use https to make connection safer.

If you are not suffering in this problem, you can try to make one: enter `https://localhost/` and same error above will occur.


## Solution

### Google Chrome

Enter `chrome://net-internals/#hsts`.
Use "Delete domain security policies". For me, I want to make localhost works again.
{% asset_img "Delete_domain_security_policies.png" "Delete domain security policies" %}

You can check if browser memorized the domain by using "Query HSTS/PKP domain".
{% asset_img "Query_HSTS_PKP_domain.png" "Query HSTS/PKP domain" %}
In my browser, `github.com` is forced https.


### Microsoft Edge

Enter `edge://net-internals/#hsts` instead. Everything else is the same. 


### Firefox

Delete history and all be fine.


# Reference

> https://hsiangfeng.github.io/other/20200723/3866554212/
> https://stackoverflow.com/questions/60558382/err-ssl-protocol-error-for-localhost-from-visual-studio-debug