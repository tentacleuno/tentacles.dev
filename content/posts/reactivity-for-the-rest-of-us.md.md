+++
title = "Reactivity For The Rest Of Us"
date = "2020-01-20"
author = "Tentacles"
description = "Observables change, variables don't."
draft = "true"
+++

Ever heard of [RxJS](https://rxjs.dev)? It's a library for creating *observables*, which are a bit like `Promise`s, except they can change over time. I've written a X-part series on how you can master RxJS, and observables in general. I talk about performance, composability, compatibility, and more.



## Composability

So, you might be thinking: **what's the point of this?** Well, to answer your question, Observables are *composable*. To demonstrate what I mean, let's take a look at the following exampFrom the subscriber, log the event to the console:.

```ts
import { Observable } from 'rxjs';
import { map } from 'rxjs/operators';

export const number$ = new Observable(subscriber => {
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
});

number$.pipe(
  map(number => number * 2)
).subscribe({
  next: number => console.log(number)
});
```

To explain *composability*, let's think of arrays: you take an array and iterate over it. Let's do the same thing as above, but using arrays.

```ts
const array = [1, 2, 3];

array
  .map(number => number *2)
  .forEach(number => console.log(number));
```

Can you see the similarities? You could say an Observable is an array, but you don't get all the values at once. Plus, there's no fixed length.

The beauty of composability means you can do virtually anything with observables. You can filter, map, reduce, and find values.

> You could say an Observable is an array, but you don't get all the values at once.

## Operators

At the heart of observables is the `pipe` function. RxJS works through *operators*, which are called with an observable, and return an observable.

> **Our earlier example of `map`**:
> ```ts
> number$.pipe(
>  map(number => number * 2)
> )
> ```

The `map` function is an operator. When you use `pipe` (and then subscribe), the observable of numbers is passed in, and an observable with the values passed through the function is returned. **Let's implement `map` ourselves.**

```js
const map = (thru) => {
  return (sourceObservable) => {
    return new Observable(subscriber => {
      sourceObservable.subscribe({
        // Some details have been glossed over for brevity.
        
        // This is where the mapping happens!
        next: (value) => subscriber.next(thru(value))
      });
    });
  }
};
```

This was very simple to simple to implement. And, excluding a few other cases, [this is basically what the RxJS-native `map` does](https://github.com/ReactiveX/rxjs/blob/7bbd37f53397193cf1371b93c1f93b18c071474f/src/internal/operators/map.ts#L53).

## Performance

In some cases, you might experience performance problems when using this pattern. For example, 

## Is it for you?

*Make sure RxJS fits your project.* If it doesn't, you'd be better off without it. RxJS is useful for composable streams of data, especially ones with no fixed length, such as API's. 

## Push me, Pull me!

RxJS features a *push* system, where the source of events dispatch events themselves (think `subscriber.next`). Unlike other systems like iterators, where the consumer has to call `next` to get an event, your observable does. 

In most cases, this simplifies the dispatching of events. 

However, unlike iterators or generators, you cannot send data from your listener to your observable. This can make some things harder to reason about (add examples here).

---

Observables compile asynchronous events, composability and declarative programming into one box. It's nice. **Get inside the box.**




<!--stackedit_data:
eyJoaXN0b3J5IjpbOTY0MDMyODAxLC0xMDYyNzYxNjc3LC0zMj
M0OTU1NzYsNDE3MDQ5NTcwLC0xMjc4NzA2MDM1XX0=
-->