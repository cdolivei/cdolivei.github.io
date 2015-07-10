---
layout: post
title: Linux Mint 17 Update
summary: An experience updating Linux Mint
tags: lyrics mint
---

So I updated Linux Mint from 16 to 17. Now Linux Mint is a bit unusual in that it will not automatically upgrade you to the latest version or even tell you that a latest version is out (I was wondering why for 2 months I got almost no new updates). Rather than packaged-based updates, what they recommend instead is that you burn a live CD, try it out, and [install the new version over your old version] [1].

Now of course you lose all your settings, and packages you installed, and have to back-up all your data (which of course you were doing anyways, right?).

The only reason I actually bothered with the upgrade is because 16 has a ridiculously old mono version - something from like 2011, and doesn't work correctly with NuGet, which I need to build a nuget package. So lots of [yak shaving] [2].

So I install Linux Mint on a USB and boot it up. Now I had a choices of wiping my entire drive, reinstall over my old OS, or I can repartition the table. I was feeling adventurous and repartitioned so at least next time it won't wipe out my data.

It was a quick install, I log in and greeted with a welcome message. One of them was "Important Information". Curious I clicked, which took me to a web page with Known Issues. First on that list:

["In the installer, "Replace OS with Linux Mint" means erase the entire drive"] [3]

Which is a problem when you have a dual-boot computer. What kills me even more is that was that this was a bug in 16 version as well ._.

[1]: http://community.linuxmint.com/tutorial/view/2 
[2]: https://en.wiktionary.org/wiki/yak_shaving
[3]: http://www.linuxmint.com/rel_qiana_cinnamon.php
