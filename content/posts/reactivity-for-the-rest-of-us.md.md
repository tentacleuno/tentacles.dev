+++
title = "Reactivity For The Rest Of Us"
date = "2020-01-20"
author = "Tentacles"
description = "Observables change, variables don't."
draft = "true"
+++

Ever heard of [RxJS](https://rxjs.dev)? It's a library for creating *observables*, which are a bit like `Promise`s, except they can change over time.

## Reactivity

**What does 'reactivity' mean?** Let's break it down: most applications respond to user input via event handlers like `onclick` or `onscroll`. When the user scrolls (or clicks) the respective event is fired, and the application does something in response. That could be loading more items in an infinite feed, or creating a new blog entry.

If you've ever worked with the DOM API's, there's a good chance you've used this fundamental feature. As these events *react* to user input, we say they have *'reactivity'*.

> Note: while it's true that some apps don't respond to user-input, reactivity can still play a crucial role in your code.

But DOM API's aren't the only way to fire / handle events in JavaScript. You could also use something like Node's `EventEmitter`, or the browser's `EventTarget` interface. There are tons of options, and RxJS is one of them.

**So, how does RxJS work?** RxJS is an implementation of *observables*, which are a bit like an `EventEmitter`, *except one 'Observable' handles one event, unlike the DOM / Node API's, where an event emitter handles thousands of events.

Let's take an example. You're creating an application for ordering food. You have a button which, when clicked, orders a pizza from your API. Firstly, we'll need to *observe* the button, by creating an *observable* which emits an event when the button is clicked. Let's see what that looks like in RxJS:

```ts
import { Observable } from 'rxjs';

const button = document.querySelector('#button');

const click$ = new Observable(subscriber => {
   button.addEventListener('click', event => subscriber.next(event));
});
```

> *Note: RxJS already has a utility for listening to DOM events, but I've not used that here to give a better overview of how this works.*

 You're probably wondering what all that means. Let's go over it.

Firstly, we're grabbing a reference to our DOM button, so we can bind an event handler to it:

```js
const button = document.querySelector('#button');
```

Next, we're creating an *observable* using the `Observable` constructor:

```js
const click$ = new Observable(subscriber => {
   button.addEventListener('click', event => subscriber.next(event));
});
```

You've probably assumed the callback passed to `Observable(...)` is called immediately. **You'd be wrong.**

> This is also known as *lazy execution*.

Until we actually *use* the observable, no event handlers are added to the button. So, how do we *use* an observable? **Easy.** Let's keep using the same code, and modify it a bit.

```ts
import { Observable } from 'rxjs';

const button = document.querySelector('#button');

const click$ = new Observable(subscriber => {
   button.addEventListener('click', event => subscriber.next(event));
});

click$.subscribe({ next: event => console.log(event) });
```

See what we did? We **subscribed** to our observable. Now, when you click the button, the event is logged to the console. This all works because when you *subscribe* to an observable, the callback passed to `Observable(...)` is called. By default, if you call `subscribe` twice, the 'click' event will have two subscribers. **Subscribes aren't shared.**

**What's a subscriber?** See what we pass to 'subscribe'? That's a *subscriber*. We can add methods to our subscriber object, which are called when the callback to `Observable` calls them, like `subscriber.next()` in our example.

We've been moving pretty quickly, so let's step back into an abstract overview: in the callback to `Observable`, we:

- Attach an event listener to our button's 'click' event,
- Call the subscriber's `next` method when a 'click' event is fired
- Log the event from our `next` method

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

---

Observables compile asynchronous events, composability and declarative programming into one box. It's nice. **Get inside the box.**




<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk4MzE4MDgwNCw0MTcwNDk1NzAsLTEyNz
g3MDYwMzVdfQ==
-->