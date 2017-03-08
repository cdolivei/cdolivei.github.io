---
layout: post
title: Resiliency in cloud applications
tags: cloud
---

My mind has been thinking about a few events that happened during the past week at work. These events range from Amazon AWS S3 going down to some errors in our application that was causing a "this should never happen" to.. happen. I have been catching up MSDN's [Cloud Design Patterns][cloudpatterns] to see what can we do about it because all the events had the same basic problem - how do we deal with services going down?

Resiliency is an easy thing to forget partially because we are accustomed to incredibly high uptimes in our infrastructure. But even some of the best in the industry make [mistakes][awscloud], and network outages, database downtime, and failures still happen. Our code must be able to catch and deal with these issues.

I am reminded about how difficult it is to code to that. It is not something that can be solved in a design pattern. It is about inspecting every point of your system that makes an external call and saying "what if this calls fails?" and being able to recover from that. It's incredibly tedius. You will inevitably try to convince yourself that the odds are extremely low. The truth is it's almost certainly going to happen. Luck is never on your side when the enemy is time.

I also reflect on how important it is to think about this early in the process because dealing with failure gracefully might require building things differently.

[cloudpatterns]: https://msdn.microsoft.com/en-us/library/dn568099.aspx
[awscloud]: https://aws.amazon.com/message/41926/
