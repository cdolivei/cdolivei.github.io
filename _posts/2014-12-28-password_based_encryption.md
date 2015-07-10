---
layout: post
title: Password Based Encryption
summary: Password based Encryption in Python
tags: tech python
---

It is often wise advice in the Software Development world to avoid rolling out your own thing and re-use what other people have done.
While maybe I don't always agree with that, I certainly always agree with it when it comes to security!

So I hit a problem where I needed to encrypt something based on a password. After some research, the correct way to solve this
problem is using [PKCS #5]. It basically salts and applied a hash many hundreds (or thousands) of times to produce a [derived key][PBKDF2].

The best solution I found was [py-bcrypt], but unfortunately was lacking in the documenation department. I had to check the source code
but eventually found my solution [in the README][README] of their code.

{% highlight python %}
import bcrypt

salt = bcrypt.gensalt()

# apply the hash function 100 times and generate a 256-bit key
key = bcrypt.kdf(password, salt, 100, 256/8)
{% endhighlight %}

One caveat: py-bcrypt does require you to compile the module before you can install it. So `pip install py-bcrypt` doesn't cut it. But I found this to be true of every python-based cryptography library because they wrap C libraries... with the exception of [python-bcrypt]. Leave it to Wenzel to be that exception to the rule.

 [PKCS #5]: http://www.emc.com/emc-plus/rsa-labs/standards-initiatives/pkcs-5-password-based-cryptography-standard.htm
 [PBKDF2]: https://en.wikipedia.org/wiki/PBKDF2
 [py-bcrypt]: https://pypi.python.org/pypi/py-bcrypt
 [README]: https://code.google.com/p/py-bcrypt/source/browse/README
 [python-bcrypt]: https://github.com/fwenzel/python-bcrypt
