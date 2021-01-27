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

function subscribe (observable, { 
  next = nothing,
  error = nothing,
  complete = nothing
}) {
  let currentEvent;
  let lastEvent;
  
  while (currentEvent = observable(lastEvent) {
    if (currentEvent) {
    
   }
  }
}
  
  return 
}



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc1NTA4MjM2MywtMTIwNDgyMzAxOCw2MD
M0NTIyMzAsLTYwNDY3ODAyNF19
-->