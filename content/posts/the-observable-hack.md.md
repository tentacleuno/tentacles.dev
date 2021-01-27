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
  next: baseNext = nothing,
  error: baseError = nothing,
  complete: baseComplete = nothing
}) {
  
  observable$.factory({ next, error, complete });
  
  return function () {
    
  }
}
  
  return 
}



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDA0OTUyNDEyLC0xMjA0ODIzMDE4LDYwMz
Q1MjIzMCwtNjA0Njc4MDI0XX0=
-->