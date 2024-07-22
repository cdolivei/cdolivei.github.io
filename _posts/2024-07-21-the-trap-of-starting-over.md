---
layout: post
title: The trap of starting over
tags: software
---

A lifetime ago, I was working on a particularly messy codebase (honestly, it was the worst codebase I ever worked on), and one of the things I was doing was cleaning it up - removing unused code. My manager at the time stopped me, and gave me this piece of advice that has stuck with me for many many years:

"Don't build your house on a foundation of cow poop"

In other words, you cannot improve something that is architecuturally broken. I didn't understand it at the time, but it is something I better appreciate now.

I currently work on projects that are old - very old. More than 20 years old. It has it's technical debt. It can definitely be a lot worse, but we've largely trapped ourselves in how we can modernize it. We've made some attempts, like containerize certain parts - but they failed. We cannnn do it, but not in a meaningful way, and it will cost us more money.

Our latest attempt was to work side-by-side with Microsoft's .NET. Our application is in the .NET Framework, which is being superceded by .NET - Microsoft's cross-platform runtime. There is some compatibility between these two, and this was exciting for us partially because it gave us the opportunity
