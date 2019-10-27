---
layout: post
title: Updating GPG subkey expiration on the YubiKey
tags: gpg
---

(One test to know whether you truely understand something is by trying to explain it. Please be aware I don't truely understand GPG)

If you read my last post on [GitHub commits]({% post_url 2019-03-14-github %}) you will probably be completely unsurpised that I (sometimes) sign my commits now. I mainly do gpg signing at work using a [YubiKey]. The way I have it setup is I created a subkey, and exported that subkey to my YubiKey. I also put an expiration of 3 months on my subkey. The idea being that, if you don't do this often enough you'll forget about it.

Soooo 3 months later and (surprise) I definitely forgot how I update my expired subkey. I eventually figured it out, so here it goes:

0. Take your YubiKey and put it aside
1. Go to your machine that has the master key.
2. run `gpg2 --edit-key cesar`
3. Select the key you want to update: `key 514EBCC933245B8E`
4. Type `expire` and follow the prompts
5. Export your key with the new expiration dates `gpg2 --export cesar`
6. Import your key into your work computer

I spent a lot of time between steps 4 and 5. My understanding was that my GPG key was on the YubiKey, and I was trying to import the key into the YubiKey. This is not true. My signing private key is on the YubiKey. It does not have the concept of expiration.

[YubiKey]:https://www.yubico.com/
