---
layout: post
title: Future of Safe Add-on
tags: firefox, safe
---

For the last few years I have been poorly maintaining the [Safe add-on for Firefox][safe]. A quick summary: it's changes the border of a page and tab colour of secure websites - green for sites with EV certificates, blue for regular SSL, and red for broken SSL. For me, it gave a better visual cue to whether I was on a secure page rather than looking for the lock icon. It's an addon that you don't know you have until you feel something's missing.

With the soon-to-be-released [let's encrypt][letsencrypt] coming, it gave me pause as to whether pervasive SSL is coming and what that means for the future of the add-on. Some people wish their projects will always stay relevant, but not me - or at least not this. A future where information is private from my machine to a server, whether it be in a trusted place like my home or in a shop's open wifi, is a future that I would gladly put that add-on to rest.

(OTOH, maybe it would be put to rest without me. Hear about [Firefox revamping their add-on ecosystem?][webextensions] :) )


[safe]: https://addons.mozilla.org/en-US/firefox/addon/safe/
[letsencrypt]: https://letsencrypt.org/
[webextensions]: https://blog.mozilla.org/addons/2015/08/21/the-future-of-developing-firefox-add-ons/
