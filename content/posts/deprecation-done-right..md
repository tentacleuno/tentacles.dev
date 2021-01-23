+++
title = "Deprecation Done Right"
date = "2020-01-23"
author = "Tentacles"
description = "The elegance of annoyance."
draft = "true"
+++

There's nothing quite like the feeling of releasing a new major version of your library. Ahh, that new package smell.

Then, the problem: **deprecation*. The old version included a hard-to-use, overcomplicated API. In retrospect, you were rushing to release the first version, so you glossed over it.

So, how *do* we deprecate an API? Should you...

- Remove the API immediately? #DontCare
- Replace the API with a stub that throws a runtime error?
- Log a warning to the console upon invocation?

This all depends on how your application is released. Some libraries like React gradually deprecate functions, by incrementally adding warnings, stubs, and fake return values (after 2 releases). 

If your package is geared around a stable API, you probably shouldn't immediately drop an API. In some cases, the best way to remove an API is to leave it in.

Another method would be to change the *naming scheme* of deprecated functions. In React, most unstable / outdated API names are prefixed with `UNSAFE_`. This gives consumers a friendly warning that they probably shouldn't be using this API!

So, to answer the main question, you need to decide *how* to manage deprecation for your library. If it's a high-profile FOSS project, you'll most likely want to gradually deprecate functions. This leads to less issues (I mean that in both the literal and Git-forge sense).

Anyway, the way I do it in JavaScript is with a little function. Start small:

```js
function deprecate (func, replacement, funcName = func.name) {
  const message = `${funcName} is deprecated.${replacement ? ` Please use ${replacement} instead.` : ''}`;
  let isFirstInvocation = true;
  return function (...args) {
     if (isFirstInvocation) {
       console.log(message);
       isFirstInvocation = false;
     }
     
     
   }
}
```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE5MTU4NTU3Nl19
-->