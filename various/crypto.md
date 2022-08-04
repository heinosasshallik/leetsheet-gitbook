---
description: Also ciphers
---

# Cryptography

## Vignere Cipher&#x20;

If you know some ciphertext and you know the corresponding plaintext, then you can use [this website](https://www.dcode.fr/vigenere-cipher) to get the key. Just input the ciphertext into the ciphertext field and the corresponding plaintext into the “knowing the key/password” field. The result will be the actual key used to cipher the text.&#x20;

The key will be repeating (it will be the same length as the ciphertext). For example, in the Brainfuck hackthebox lab, the result was FUCKMYBRAINFUCKMYBRAINFUCKMYBRAIN, meaning the key is FUCKMYBRAIN.

## Hash Length Extension Attack <a href="#docs-internal-guid-a02cfd00-7fff-9dea-9969-7a0c41b8c82e" id="docs-internal-guid-a02cfd00-7fff-9dea-9969-7a0c41b8c82e"></a>

{% embed url="https://blog.skullsecurity.org/2012/everything-you-need-to-know-about-hash-length-extension-attacks" %}

An application is susceptible to a hash length extension attack if it prepends a secret value to a string, hashes it with a vulnerable algorithm, and entrusts the attacker with both the string and the hash, but not the secret. Then, the server relies on the secret to decide whether or not the data returned later is the same as the original data.

It turns out, even though the attacker doesn't know the value of the prepended secret, he can still generate a valid hash for `{secret || data || attacker_controlled_data}`
