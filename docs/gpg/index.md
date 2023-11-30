---
layout: default
title: GPG
nav_order: 2
has_children: true
permalink: /docs/gpg
---

# Overview

The **G**NU **P**rivacy **G**aurd (GPG) is an open source implementation of the OpenPGP encryption standard with some improvements. In essence, GPG is a type of public-key cryptography that allows you to encrypt messages that can only be decrypted by specified people (more in-depth explanation about GPG and public-key cryptography [here](https://en.wikipedia.org/wiki/Public-key_cryptography)).

GPG and other public-key cryptography uses key pairs to encrypt and decrypt files/messages. Each key pair consists of a public and private key which can readily be generated using the GPG installation detailed later. As suggested in the name, your public key can (and should) be readily shared across the internet between friends. Your private key on the other hand is secret and should be treated like a password. If anyone gets a hold of your private key, they can encrypt and decrypt your private messages/files.

So how does it work? Consider two friends Alice and Bob where Alice wants to send bob a secret message without anyone being able to decipher it. First, Bob sends Alice his public key through an insecure method of communication such as an email or through a chatroom. Alice then uses Bob's public key to encrypt her message; the result is a scrambled mess of symbols that can be sent back to Bob using the same insecure methods as before. This encrypted message can only be decrypted with Bob's private key.

The utility of public key cryptography lies within the ability to send secure messages across the internet that only specific people can read. The public key is like a locked mailbox; anyone can send mail to it but only the person with the key can read the mail.

![Public key cryptography flowchart](../assets/images/public_key_cryptography.png)
*Source: [Twilio](https://www.twilio.com/blog/what-is-public-key-cryptography)*

The other main utility of GPG and public key cryptography is confirming that a message originated from a certain person and was not altered in transit. You can sign a message with your private key which is the equivalent of putting your signature on the message. Any recipients can compare that signature to your public key; if the signatures match, then we can say for certain that the message did originate from the sender and that it was not altered by any malicious third parties.

