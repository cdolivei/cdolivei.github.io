---
layout: post
title: Passwordless Password
tags: password
---

Humour me.

Imagine I wanted to sign-up for Bob's coffee roasters website<sup>1</sup> to order some flavourful roasted beans<sup>2</sup>. I click sign-up button, enter my e-mail address and shpping information, and then told to go to my e-mail account to verify my e-mail account. At no point was I asked to enter a password.

I log into my e-mail account and click the verification link, the website then sets a password in my browser's localstorage. I am assigned a session cookie, and can browse the website normally.  I close my browser, relaunch, and visit the website again. I enter my e-mail. The browser takes the password from local storage, and submits it.  If the password for any reason is invalid, I must re-verify my email. Otherwise, it lets me in.

#### Whyyyyy?

Two reasons

1. Password managers are ([usually][lastpass]) amazing and incredibly useful, and I would recommend it over this approach for sure (my reasons why are below). That said, I don't know how popular password managers are to the general public.
2. I read something on, I believe it was hacker news, a comment that talked about a website that only used email to authenticate the user. Apparently customers loved it. I thought that was amusing (and frightening) and wondered if that kind of experience can actually exist securely.

#### What happens if I change devices

The same thing. You must go to your email account and verify. You would also need to store a device ID so you can map passwords to devices.

#### What happens if I lose my device?

This is probably fine, minus the loss of your device. Yes, technically anyone with access to your <strike>device</strike> browser has access to your passwords. But given that your device (phone, laptop) probably has unrestricted access to your email, anyone can just use the standard password reset. When an attacker has access to the device, generally it's lost cause and you cannot trust that device.

Devices often have PINs, fingerprint readers, passwords, and encrypted drives. That is what should prevent them from accessing your private data.

#### Caveats

If you're site has an XSS vulnerability, it's game over. This is by far the biggest downside I see with this approach. There are [mitigaton techniques][owasp], but you have to be perfect 100% of the time. (XSS is pretty bad even if an attacker wouldn't be able to steal your password, but password is pretty much winning gold).

Some other caveats I see:

1. Devices need access to email
2. Browser support for local storage
3. Private browsing may [affect access to local storage][safari]
4. You still need to protect the password in the database
5. Devices/browser shared between multiple people
6. If a user has multiple accounts, that may complicate things a bit

<sup>1</sup>: My imagination is shot and some coffee would be good right now

<sup>2</sup>: Man, I can realllly go for a coffee

[owasp]: https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)
[lastpass]: https://blog.lastpass.com/2017/03/important-security-updates-for-our-users.html/
[safari]: https://stackoverflow.com/questions/14555347/html5-localstorage-error-with-safari-quota-exceeded-err-dom-exception-22-an
