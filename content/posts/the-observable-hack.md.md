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

function Throw (error) {
  return { type: 'error', error };
 }
 
 function Next (value) {
   return { type: 'next', value };
 }

function Complete () {
  return { type: 'complete' };
}

async function* subscribe (observable, { 
  next = nothing,
  error = nothing,
  complete = nothing
}) {
  let currentEvent;
  let lastEvent;
  let subscribed = true;
  
  while (subscribed && currentEvent = await observable(lastEvent)) {
    switch (currentEvent.type) {
      case 'error': yield error(currentEvent.error); break;
      case 'complete': yield complete(); subscribed = false; break;
      case 'next': yield next(currentEvent.value); break;
   }
   
   lastEvent = currentEvent;
  }
}
}



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc0OTE3NjYwMCwtMTIwNDgyMzAxOCw2MD
M0NTIyMzAsLTYwNDY3ODAyNF19
-->