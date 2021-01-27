+++
title = "Deprecation Done Right"
date = "2020-01-23"
author = "Tentacles"
description = "The elegance of annoyance."
draft = "true"
+++

So, observables. They're

```js
function nothing () {}

function observable (factory) {
  return { factory };
}

function subscribe (observable$, { 
  next = nothing,
  error = nothing,
  complete = nothing
}) {
  observable$.factory({ next, error, complete });
  
}
  
  return 
}



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3ODc1NTA4MDgsLTEyMDQ4MjMwMTgsNj
AzNDUyMjMwLC02MDQ2NzgwMjRdfQ==
-->