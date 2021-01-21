+++
title = "Reactivity For The Rest Of Us"
date = "2020-01-20"
author = "Tentacles"
description = "Observables change, variables don't."
draft = "true"
+++

Ever heard of [RxJS](https://rxjs.dev)? It's a library for creating *observables*, which are a bit like `Promise`s, except they can change over time.

**What does 'reactivity' mean?** Let's break it down: most applications respond to user input via event handlers like `onclick` or `onscroll`. When the user scrolls (or clicks) the respective event is fired, and the application does something in response. That could be loading more items in an infinite feed, or creating a new blog entry.

If you've ever worked with the DOM API's, there's a good chance you've used this fundamental feature. As these events *react* to user input, we say they have *'reactivity'*.

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

So, you might be thinking: **what's the point of this?** Well, to answer your question, Observables are *composable*. To demonstrate what I mean, let's take a look at the following example:

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







-  
<!--stackedit_data:
eyJoaXN0b3J5IjpbODU5MTA0NzA3LDk2MjE5ODA5MF19
-->