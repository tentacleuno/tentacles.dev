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

If your package is geared around a stable API, you probably shouldn't immediately drop an API. In some cases, the best way to remove an API is to 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgyNDMyMDUxMF19
-->