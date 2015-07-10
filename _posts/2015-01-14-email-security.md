---
layout: post
title: E-mail security
summary: Some thoughts on e-mail encryption
tags: tech email security
---

A number of weeks ago someone pointed me to [darkmail] which was started by the same people who ran [Lavabit] before it shutdown.

I thought "this sounds great!... if it works"

Sadly I do not know how it works without reading the specification. The website is pretty bare, as is the wikipedia article (at the time of this writing). But I have used, and have a general understanding of, <acronym title="Pretty Good Privacy">PGP</acronym> and S/MIME. Both of which have not seen really great adoption, and remain pretty niche products.

There was an interesting post on the [planet Mozilla] by Joshua Cranmer, who works on various parts of the [Mozilla Mail module], gave his opinion on [why e-mail security failed][post]. While I have not come across many of the problems (which I probably would if more people used it) he points out, one issue he does point that I think is pretty major is the fact that you cannot do server-side searching and SPAM filtering on a pure end-to-end encryption model.

So it would be interesting to see whether and how Darkmail solves this issue. Or whether we would have to accept sacrifices in security for more usability.

 [lavabit]: https://en.wikipedia.org/wiki/Lavabit
 [darkmail]: http://darkmail.info/
 [planet Mozilla]: http://planet.mozilla.org
 [Mozilla Mail module]: https://wiki.mozilla.org/Modules/MailNews_Core
 [post]: http://quetzalcoatal.blogspot.ca/2015/01/why-email-is-hard-part-8-why-email.html
