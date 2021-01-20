+++
title = "The Dangers Behind OAuth"
date = "1986-09-17"
author = "Elliot"
cover = "img/hello.jpg"
description = "\"Hello, friend?\" That's lame. Maybe I should give you a name?"
+++

At first sight, OAuth is great: you can defer the worries of storing passwords to another website, making it a prime target for novice and experienced web developers alike. But it's not all good.

While OAuth *does* somewhat improve security, by removing the burden of managing passwords from the developer, it does have plenty of downsides. One of them, as more and more people are beginning to realise, is **privacy**. 

By giving an external company control over your authentication flow, you're putting a substantial amount of power in their hands. For starters, if a user's account were to be removed, they would also lose access to your service. Another example is data control; neither you, or your users, actually *own* the authentication flow. 

This means you have to entirely trust your OAuth provider. The skeptics in us would call this an *impossible goal*. If you don't own the server, you can't trust it. You don't *know* what's happening "behind the scenes".

> “Trust yourself, you know more than you think you do.” – Benjamin Spock

So, if we can't trust server providers, who *can* we trust?

**Ourselves**.

While handling authentication does carry its own level of complexity, it's *everywhere*. Instead of rolling your own layer, 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQwMTY0NDQxNl19
-->