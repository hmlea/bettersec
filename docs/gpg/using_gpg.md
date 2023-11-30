---
layout: default
title: Using GPG
parent: GPG
nav_order: 2
---


# Generating a Keypair

Now that GPG is installed, we can start using it. First we need to create our own keypair; to do this we will start with the `gen-key` command:

```
gpg --full-gen-key
```

This allows us to generate a keypair with extended options; utilizing these options we can make our keys exceptionally secure, to the point that they will not be able to be cracked for potentially millions of years with todays computing power.

You will be prompted with a bunch of different options; the only one we want to worry about it `(1) RSA and RSA`. To select this, type a `1` followed by enter. The other options are other encryption algorithms that we won't worry about.

After, you will be prompted with a question asking your desired key size:

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want?
```

The longer the keysize, the more secure the encryption; type `4096` and press enter.

Next it will ask how long your key will be valid for. Once your key expires, it can't be used to verify signatures anymore. It is personal preference for how long you want your key to be valid for, but is good practice to generate new keys every so often. I personally create keys that are valid for 1 year by typing `1y` and pressing enter. Confirm this with `y`.

It will then ask you for information that will be attached to your key. Use your real name and email. The comment can be whatever you want; I tend to leave it blank. After, it will have you confirm your information. You can type `o` to confirm or go back and change it.

Lastly, it will ask you for a password. This password will be used to access your secret key as well as encrypt, decrypt, and sign. **It is imperative to choose a strong password that you don't use for any other service**. Write it down on paper or store it someplace safe (see the KeePassXC tutorial). After confirming your password a few times, a summary of your newly generated key will be displayed; it will look something like this:

```
gpg: revocation certificate stored as '~/.gnupg/openpgp-revocs.d/A122BE67EF5F2A1F73FE4442840F0E58D25D350C.rev'
public and secret key created and signed.

pub   ed25519 2023-04-09 [SC] [expires: 2024-04-08]
      A122BE67EF5F2A1F73FE4442840F0E58D25D350C
uid                      Hayden Leatherwood <hmleatherwood@gmail.com>
sub   cv25519 2023-04-09 [E] [expires: 2024-04-08]
```

Most information above is self exlanatory except for the random string of letters and numbers above my name. This is the fingerprint of your key; just like a real fingerprint, it serves as a unique identifier of your key.

# Importing, Exporting, and Trusting

Now that you have your own keypair, you need to build your network in order to encrypt, decrypt, and sign messages. To share your key with someone, you need to export it. To do this, the base command is:

```
gpg --armor --export [key identifier]
```

The *key identifier* can be any piece of information associated with your key, such as the name, fingerprint, or email; GPG does a good job of matching it and exporting the right key, but I usually do email. To export my own public key, I would use:

```
gpg --armor --export hmleatherwood@gmail.com
```

This command would show my public key in the terminal window; it looks like this:

```
-----BEGIN PGP PUBLIC KEY BLOCK-----

mDMEZDNFxRYJKwYBBAHaRw8BAQdAeLjv4Xmx1/ncYxz/oBDfSMXq+eC9Uc7LH/rq
dW5CVru0LEhheWRlbiBMZWF0aGVyd29vZCA8aG1sZWF0aGVyd29vZEBnbWFpbC5j
b20+iJoEExYKAEIWIQShIr5n718qH3P+REKEDw5Y0l01DAUCZDNFxQIbAwUJAeEz
gAULCQgHAgMiAgEGFQoJCAsCBBYCAwECHgcCF4AACgkQhA8OWNJdNQycLgEA658b
npJsUUlqzUdCBeqL9uS4Yhdh/D2eHrvgGR9giawBAOcnO4cadYEsa0maXc9uRGxw
q9cjjMfQZpDf3u14ixQMuDgEZDNFxRIKKwYBBAGXVQEFAQEHQKQAnmjBZ+qa8S0I
jsDhQj/fNYJtJ/T6vbvdtvjlw59DAwEIB4h+BBgWCgAmFiEEoSK+Z+9fKh9z/kRC
hA8OWNJdNQwFAmQzRcUCGwwFCQHhM4AACgkQhA8OWNJdNQzHuQEAvKVDrxCbIsmO
PVL0DtLr18nAkErBuCZsZ/JXItV519oBAPw8dmNeW9TEIM0WXTvQsQaGFLBZpB4y
O3jVEshqoWUG
=+UfO
-----END PGP PUBLIC KEY BLOCK-----
```

This can be directly copied and imported (detailed below) or it can further be exported to a file. To export it to a file, we need to add the `--output` flag. For example, if I wanted to export it to a file called `pubkey.txt` I would use:

```
gpg --armor --output pubkey.txt --export hmleatherwood@gmail.com
```

Note that this file should always end in `.txt` and will be saved to the current directory in the terminal. This directory can be seen with the `pwd` command.

Now lets import my public key to your keyring (you can also download the key file directly from the site repository [here](../../pubkey.asc)). Your keyring is like you address book; you need a key in your keyring to encrypt a message to them (just like you need someone in your address book to send them a text). One way to do this is to copy and paste: type `echo "`, paste the key, then type `" | gpg --import`. It should look like this:

```
echo "-----BEGIN PGP PUBLIC KEY BLOCK-----

mDMEZDNFxRYJKwYBBAHaRw8BAQdAeLjv4Xmx1/ncYxz/oBDfSMXq+eC9Uc7LH/rq
dW5CVru0LEhheWRlbiBMZWF0aGVyd29vZCA8aG1sZWF0aGVyd29vZEBnbWFpbC5j
b20+iJoEExYKAEIWIQShIr5n718qH3P+REKEDw5Y0l01DAUCZDNFxQIbAwUJAeEz
gAULCQgHAgMiAgEGFQoJCAsCBBYCAwECHgcCF4AACgkQhA8OWNJdNQycLgEA658b
npJsUUlqzUdCBeqL9uS4Yhdh/D2eHrvgGR9giawBAOcnO4cadYEsa0maXc9uRGxw
q9cjjMfQZpDf3u14ixQMuDgEZDNFxRIKKwYBBAGXVQEFAQEHQKQAnmjBZ+qa8S0I
jsDhQj/fNYJtJ/T6vbvdtvjlw59DAwEIB4h+BBgWCgAmFiEEoSK+Z+9fKh9z/kRC
hA8OWNJdNQwFAmQzRcUCGwwFCQHhM4AACgkQhA8OWNJdNQzHuQEAvKVDrxCbIsmO
PVL0DtLr18nAkErBuCZsZ/JXItV519oBAPw8dmNeW9TEIM0WXTvQsQaGFLBZpB4y
O3jVEshqoWUG
=+UfO
-----END PGP PUBLIC KEY BLOCK-----" | gpg --import
```

`echo` prints the key to the terminal, and `|` (pipe) passes it to the `gpg --import` command. If done correctly, you'll get a message saying the key was imported:

```
gpg: key 840F0E58D25D350C: public key "Hayden Leatherwood <hmleatherwood@gmail.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1
```

If the key is exported to a text file (say `pubkey.txt`), it can be imported simply by appending the files name to the `--import` flag:

```
gpg --import pubkey.txt
```

My key should now be in your keyring. You can confirm this with `gpg -k`, which should list all keys in your keyring including mine. It should look like this:

```
pub   rsa4096 2023-11-29 [SC] [expires: 2023-12-06]
      F0DB914EB63858F309C55F13D0ED22B5643803B4
uid           [ultimate] YOUR_KEY <YOUR@EMAIL.com>
sub   rsa4096 2023-11-29 [E] [expires: 2023-12-06]

pub   ed25519 2023-04-09 [SC] [expires: 2024-04-08]
      A122BE67EF5F2A1F73FE4442840F0E58D25D350C
uid           [ unknown] Hayden Leatherwood <hmleatherwood@gmail.com>
sub   cv25519 2023-04-09 [E] [expires: 2024-04-08]
```

To the left of your key, you can see the text `[ultimate]`. This is the validity of the key. We can get more info if we go edit the key with the following command:

```
gpg --edit-key hmleatherwood
```

This will bring up the following information:

```
pub  ed25519/840F0E58D25D350C
     created: 2023-04-09  expires: 2024-04-08  usage: SC  
     trust: unknown       validity: unknown
sub  cv25519/A826B3490E9A522F
     created: 2023-04-09  expires: 2024-04-08  usage: E   
[ unknown] (1). Hayden Leatherwood <hmleatherwood@gmail.com>
```

Here we can see the vailidity as `unknown` (just like we saw above) as well as another attribute, `trust`, which is also unknown. While similar, trust and validity are fundamentally different. First, validity describes whether the key is the correct key and actually belongs to the person it says it does. Trust on the other hand describes how much you actually trust the person that holds the key. A key can be valid but not trusted (say if the key belonged to an aquantance who you know but don't really trust), but not vice versa.

You can directly set the trust level of individual keys based on how much you trust the key holder (described below). Validity is set by singing a key yourself, or if a key is signed by another key that you fully trust.

Trust and validity is a much more complicated topic than explained here and I urge you to read more about it if you would like (see [here](https://www.gnupg.org/gph/en/manual.html#FTN.AEN378) and [here](https://superuser.com/questions/1312139/gnupg-key-validity)).

Let's start by setting the trust of my key. Since you know I am the key holder and you trust me, we want to fully trust my key. While still in the `--edit-key` screen, we can type `trust` to edit the trust level; this will bring up this prompt:

```
Please decide how far you trust this user to correctly verify other users' keys
(by looking at passports, checking fingerprints from different sources, etc.)

  1 = I don't know or won't say
  2 = I do NOT trust
  3 = I trust marginally
  4 = I trust fully
  5 = I trust ultimately
  m = back to the main menu
```

Since you trust me, we will type `4` to fully trust my public key. **Note that you should never ultimately trust a key that is not yours**; a good rule of thumb is to never set a key to level 5 trust. Also only fully trust keys that you can confirm belong to the owner.

After setting the trust, we want to validate my key. This basically reaffirms GPG that my key is safe and will help us down the road. To sign it, we can use the `sign` command in the `--edit-key` prompt. It will have you confirm you want to sign the key by typing `y` and entering you password. After, you can save the changes by typing `quit` followed by `y`. Now if you list your keys with `gpg -k` you will be able to see the changes:

```
pub   rsa4096 2023-11-29 [SC] [expires: 2023-12-06]
      F0DB914EB63858F309C55F13D0ED22B5643803B4
uid           [ultimate] YOUR_KEY <YOUR@EMAIL.com>
sub   rsa4096 2023-11-29 [E] [expires: 2023-12-06]

pub   ed25519 2023-04-09 [SC] [expires: 2024-04-08]
      A122BE67EF5F2A1F73FE4442840F0E58D25D350C
uid           [  full  ] Hayden Leatherwood <hmleatherwood@gmail.com>
sub   cv25519 2023-04-09 [E] [expires: 2024-04-08]
```

We can see that my key is valid and fully trusted with the text. Now we can validate my signatures and messages as well as encrypt messages to me.

# Encrypting, Decrypting, and Validating

With my key in your keyring, lets validate a signed message. To do this, we need to sign a message. You first write your message in a `.txt` file. An easy way to do this is to open TextEdit, press `⌘ + ⇧ + t`, type your message, and save it with a `.txt` extension. I saved the following message as `message.txt`:

>This is a secret message written by me. I am signing it so you can confirm that it came from me and was not altered in transit. \:)

We can then now sign the message without encrypting it by using the following command:

```
gpg --clearsign message.txt
```

This will sign the file and save it to `message.txt.asc`; the `.asc` file type means that it is pure ASCII or text only. If you want to output the signed message with a different name, you can add the `--output` tag; the following command would save the file under the name `signed_msg.txt`:

```
gpg --clearsign --output signed_msg.txt message.txt
```

We can view the contents of the `signed_msg.txt` file with the `cat` command:

```
cat signed_message.txt
```

We can then see the message reads the following:

```
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA512

This is a secret message written by me. I am signing it so you can confirm that it came from me and was not altered in transit. :)
-----BEGIN PGP SIGNATURE-----

iHUEARYKAB0WIQShIr5n718qH3P+REKEDw5Y0l01DAUCZWaUagAKCRCEDw5Y0l01
DMcCAP9Y25Myd7/aehkfWUsB5HIT1UCU0rG9YrVsYeoJQoTDpgEA8xDn3qb8EKHV
m8sJxDtLpCWSCIO2A1YEReVTtfUYzA0=
=kWBk
-----END PGP SIGNATURE-----
```

Let's verify this message and confirm that it came from me and was not altered in transit. First, copy the message above and save it to a `.txt` file named `hayden_message.txt`. Then we can use the `gpg --verify` command to verify it:

```
gpg --verify hayden_message.txt
```

You need to ensure that the Terminal is in the same directory as the file; an easy way to ensure this is to type `gpg --verify ` and drag the file directly into the terminal. Doing so gives us this response:

```
gpg: Signature made Tue 28 Nov 2023 08:31:22 PM EST
gpg:                using EDDSA key A122BE67EF5F2A1F73FE4442840F0E58D25D350C
gpg: Good signature from "Hayden Leatherwood <hmleatherwood@gmail.com>" [full]
```

This tells us that the message was signed with a key we trust: my key. In short, the string of characters at the bottom of the message contains my signature and a copy of the original message; if the message was altered in transit, it wouldn't match and would give a bad response. This would be an example of the response if the text was changed:

```
gpg: Signature made Tue 28 Nov 2023 08:31:22 PM EST
gpg:                using EDDSA key A122BE67EF5F2A1F73FE4442840F0E58D25D350C
gpg: BAD signature from "Hayden Leatherwood <hmleatherwood@gmail.com>" [full]
```

So what about encryption and decryption? First lets encrypt a message to me using my public key that is now trusted in your keyring. Let's encrypt the following message:

>Hey Hayden! This GPG stuff is super cool! I have never been more secure! A++

We can put this in a `.txt` file named `to_hayden.txt`. Then we can encrypt it using my public key with the following command:

```
gpg --output to_hayden_encrypted.txt --encrypt --armor --recipient hmleatherwood@gmail.com to_hayden.txt
```

This will output the encrypted message to a file named `to_hayden_encrypted.txt`. Since the recipient was set to me, only I will be able to decrypt the file. We can see the contenets of this file using `cat to_hayden_encrypted.txt` which produces this output:

```
-----BEGIN PGP MESSAGE-----

hF4DqCazSQ6aUi8SAQdApmB7zA9Ng2x1Mu2HDwsOVoK1kEANLULrmL82WMqFgFAw
gjljwKVTET//v/6Yky60Hah4ZVHEWc/Pr2SSV3Kzpd1JCbUEqwnVzVHQDBl6qgyA
0ukB0gsjf6yYJ7YPaaQ3Bfkjoy2g+l2QddvSMj048QFkDczFPdtLjzhoIgbjsPRG
mjAY26ZwYM8D4noiT2XRgTY2T10JxDMJpT2+hr8wbO3ldeds1eAQDBg8A6k8bBNY
f3Ijyf8KPlgOYp39yYazgxZg9XhnDdIBGYnajdDl9JeqUmz9ChN7JAfJXRn/o4GE
S8vHOOUMjoPxJGJzQpg0/XB83ob1317r6mUAaiYFA4FdSb6FFFV5AGF3Fp99/0wz
gNqmj+JFetlh54TF3xJ/VKP671OBiglmWOkq4AcDgmI9X7QwOJiJAWjrGlUOrLCe
pVgjRyqtB/7yUBZe3QZPXkSCUvO8YbsbY5mAkBReu8OnS63RuYJXYnEjNTmcLTgH
MyH0SAKXOkCQKWNRXEQCZlC3AAFZWeCXkuLRftp8WzuO6DVU4gqzNNtsxI9Mi3jH
B5PSvYurRy4yRw0m6Zav+TGPkhK2Au82cP9YGHeYaFxjRaL/vGzAqHLai3bolP4o
cpfQ+zUm3+k2PsyDhak6c6zkzJx5Zld0UvxC0qXPtRwtQKFqe1FysXuZahkJYQsj
rc/FFwyi5hqg0gVPjXerNjcRmUiojZS4MaZH73ZFFfLFui0AAagC3H4nCHxS9p2F
EUmcxbaApL0y5HJaTPOy7Ud4E/hIN3qxkAkFVbyKCM8RDcAc/fmEDlT8t/nJ5S+x
aOd0I39wXGt3Z+YEed0OvfCI7x4giMLBjbuo7HXQt7qbXEMeAMvjsyghveYJdkC9
oUVihrle72GPtlOS5D6O23O4OLLFGXGVu7ylRs+jrDpWE2gKLZNyvLpy9RWQzaQ6
0wEduIuhfUtAfl2fbflIbHkYY+7TRz0nDwnZy6UJSD7lAtehDlcRzAwPNPQY7Viv
jWWNXNGv3dN8/xY+JmZrCTDljjM89qr2TLsTDRefmjyc4ru3do1gNYzXtFWA5scv
mbfBV8cVGQjEqePbw1bKEg==
=PEOf
-----END PGP MESSAGE-----
```

It looks like gibberish but on my end, I can decrypt it with my private key only. Because no one else is able to decrypt this message, it can safely be sent through insecure channels such as email, text, etc. If I copy and paste that message into a text file named `hayden_msg.txt`, I can decrypt it with the following code:

```
gpg --decrypt hayden_msg.txt
```

Decrypting the message gives me this output:

```
gpg: encrypted with cv25519 key, ID A826B3490E9A522F, created 2023-04-09
      "Hayden Leatherwood <hmleatherwood@gmail.com>"
Hey Hayden! This GPG stuff is super cool! I have never been more secure! A++
```

The encrypt command can be customized with more recipients; if you want to encrypt a message that is for Bob, Alice, and myself, you could use a command like the following (given that all 3 people are in your keyring):

```
gpg --output to_hayden_encrypted.txt --encrypt --armor --recipient bob@gmail.com --recipient alice@yahoo.com --recipient hmleatherwood@gmail.com to_hayden.txt
```

A good practice is to always sign the files you are encrypting as well. This just gives the added benefit of confirming the integrity of the encrypted message. This is as easy as adding the `--sign` flag inthe encrypt command like so:

```
gpg --output to_hayden_encrypted.txt --encrypt --armor --sign --recipient hmleatherwood@gmail.com to_hayden.txt
```

If I try to decrypt this message and do not have the sender's key in my keyring, I get a warning:

```
gpg: encrypted with cv25519 key, ID A826B3490E9A522F, created 2023-04-09
      "Hayden Leatherwood <hmleatherwood@gmail.com>"
Hey Hayden! This GPG stuff is super cool! I have never been more secure! A++
gpg: Signature made Tue Nov 28 19:05:41 2023 MST
gpg:                using RSA key F0DB914EB63858F309C55F13D0ED22B5643803B4
gpg: Can't check signature: No public key
```

I can still decrypt the message but GPG tells me that I do not have the sender in my keyring. On the other hand, if I do have the sender in my keyring, it confirms the integrity of the message:

```
gpg: encrypted with cv25519 key, ID A826B3490E9A522F, created 2023-04-09
      "Hayden Leatherwood <hmleatherwood@gmail.com>"
Hey Hayden! This GPG stuff is super cool! I have never been more secure! A++
gpg: Signature made Tue Nov 28 19:18:39 2023 MST
gpg:                using RSA key F0DB914EB63858F309C55F13D0ED22B5643803B4
gpg: Good signature from "YOUR_KEY <YOUR@EMAIL.com>" [full]
```

# Conclusion

GPG and other public key cryptography allows you to encrypt messages so they can securely be sent through insecure channels. This not only prevents malicious third parties from intercepting important information but also allows the recipient to verify that the message came from you and was not altered en route.

While using the command line interface certainly has a learning curve, it is extremely beneficial in keeping important information secure while in transit. Developers such as [GPGTools](https://gpgtools.org/) have developed graphic user interfaces that allow users to utilize GPG without the command line; however, they have more moving parts which in turn introduce more possible vulnerabilities. Additionally, I have no experience with these programs.

---

More can be read about GPG and the command line interface in the *The GNU Privacy Handbook* online [here](https://www.gnupg.org/gph/en/manual.html).

