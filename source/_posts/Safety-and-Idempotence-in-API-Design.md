---
title: Safety and Idempotence in API Design
date: 2023-02-16 15:43:53
tags:
---


{% asset_img http-methods.jpg HTTP methods %}

There are various HTTP methods. Every of them has its own semantics.
Which means each method has been defined what it should do.

Designing APIs that following semantics is important since semantics of methods has been defined in HTTP/1.1 specification.
Almost all browsers, APIs, apps, tools, and other developments are based on this consensus.
So not following it may cause issues in most scenarios.

<!-- more -->

## Safe Methods

Definition of safe methods in RFC7231:

> 4.2.1.  Safe Methods
>
> Request methods are considered "safe" if their defined semantics are essentially read-only; i.e., the client does not request, and does not expect, any state change on the origin server as a result of applying a safe method to a target resource.
> Likewise, reasonable use of a safe method is not expected to cause any harm, loss of property, or unusual burden on the origin server.

Did you saw the keyword? `Read-only`.

> A `safe method` shall not alter any state of the server. In other word, it performs `read-only` operation.

But this does not mean entirely read-only.
For example, logging will not break the definition of `safe method` though it appends data into log file.
We only concern about resource data.

> In HTTP/1.1 specification, the `GET`, `HEAD`, `OPTIONS`, and `TRACE` methods are defined to be safe.

The mostly used `safe method` must be `GET`.
For instance, you want to obtain a book detail by `GET` request `GET library/books/123456`.
This request will only retrieve book information and will not apply any changes to the server.
Unlike `DELETE library/books/123456` will remove the book which apparently change the state of server.

But why we need to determine if a method is `safe` or not?

`Safe methods` allow automated retrieval processes (spiders or crawlers) and cache performance optimization (pre-fetching) to work without any fear of causing harm.
Furthermore, allow appropiate constraints on the use of `unsafe methods`.

As the book example above, browser can cache the response retrieving from `GET library/books/123456`.
If you make the identical request again, browser will return the same response from cache.

## Idempotent Methods

Definition of idempotent methods in RFC7231:

> 4.2.2.  Idempotent Methods
> 
> A request method is considered "idempotent" if the intended effect on the server of multiple identical requests with that method is the same as the effect for a single such request.
> Of the request methods defined by this specification, PUT, DELETE, and safe request methods are idempotent.

The purpose of idempotence is to make API to be fault-tolerant, which means it is retryable.

Still we have the example `DELETE library/books/123456`.
What if the connection failed? How do we make sure that the book has been deleted?

Just re-establish a new connection and send the identical request again.
Since `DELETE` is an idempotent method, multiple identical requests make the same effect to server as a single request.

Though you may get `404` on second attempt or after if the book has already been deleted but it does not matter.

> Repeating the request will have the same intended effect, even if the original request succeeded, though the response might differ.

Also, `safe methods` like `GET`, is idempotent as well.
`Safe methods` do not alter server state at all, obviously are repeatable.

`POST` is not idempotent since multiple resources may be created if the request is sent repeatly.

# References
> https://www.rfc-editor.org/rfc/rfc7231
> https://restfulapi.net/idempotent-rest-apis/
> https://lance.coderbridge.io/2021/06/06/what-is-safe-method-and-indempotent-methods/