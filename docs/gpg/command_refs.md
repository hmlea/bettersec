---
layout: default
title: Command References
parent: GPG
nav_order: 3
---

# Table of Contents

- **[General Commands](#general-commands)**
  - [Print File Contents](#print-file-contents)
  - [Changing Terminal Directory](#changing-terminal-directory)
  - [Viewing Current Terminal Directory](#viewing-current-terminal-directory)
- **[GPG Commands](#gpg-commands)**
  - [Generating a Keypair](#generating-a-keypair)
  - [Exporting a Public Key](#exporting-a-public-key)
  - [Importing a Public Key](#importing-a-public-key)
  - [List Keys in Keyring](#list-keys-in-keyring)
  - [Editing Keys](#editing-keys)
  - [Signing Messages](#signing-messages)
  - [Verifying Messages](#verifying-messages)
  - [Encrypting Messages](#encrypting-messages)
  - [Decrypting Messages](#decrypting-messages)

# General Commands

## Print File Contents

```
cat [file name]
```

## Changing Terminal Directory

```
cd [directory]
```

## Viewing Current Terminal Directory

```
pwd
```

# GPG Commands

## Generating a Keypair

```
gpg --full-gen-key
```

Notes:
- Use the maximum key size of 4096 bits
- Have keys expire after 1 year
- Use a unique password and store it on paper where you won't lose it

## Exporting a Public Key

### To text in Terminal:

```
gpg --armor --export [key identifier]
```

### To a file:

```
gpg --armor --output pubkey.txt --export [key identifier]
```

Notes:
- [key identifier] can be fingerprint, name, email, etc.
- `pubkey.txt` can be replaced with your desired name

## Importing a Public Key

### From text:

```
echo "[public key]" | gpg --import
```

### From file:

```
gpg --import pubkey.txt
```

Notes:
- Replace [public key] with the key you want to import
- `pubkey.txt` can be replaced with the name of the key file

## List Keys in Keyring

### All public keys:

```
gpg -k
```

### All private keys:

```
gpg -K
```

Notes:
- Never export or give away your private key(s)

## Editing Keys

### Changing trust level:

```
gpg --edit-key [key identifier]
trust
```

### Signing/validating keys:

```
gpg --edit-key [key identifier]
sign
```

Notes:
- [key identifier] can be fingerprint, name, email, etc.
- Type `quit` at the end of signing/trusting to save changes
- `--edit-key` is a good command to see all key information
- Never trust a key ultimately (especially someone elses)

## Signing Messages

```
gpg --clearsign [file name]
gpg --clearsign --output [output name] [file name]
```

Notes:
- Either command can be used
- Replace [file name] with the file containing your message
- Replace [output name] with the name of the file you want to contain the signed message (ending in `.txt`)

## Verifying Messages

```
gpg --verify [file name]
```

Notes:
- Replace [file name] with the file containing your signed message

## Encrypting Messages

### Encrypting only:

```
gpg --output [output name] --encrypt --armor --recipient [recipient key id] [file name]
```

### Encrypting and signing:

```
gpg --output [output name] --encrypt --armor --sign --recipient [recipient key id] [file name]
```

### Encrypting for multiple recipients

```
gpg --output [output name] --encrypt --armor --recipient [recipient key id 1] --recipient [recipient key id 2] [file name]
```

Notes:
- Replace [output name] with the name of the file you want to contain the signed message (ending in `.txt` or `.gpg`)
- Replace [recipient key id] with the fingerprint, email, name, etc. of the recipient's key
- Replace [file name] with the file containing your signed message
- It is good practice to always sign your encrypted messsages

## Decrypting Messages

```
gpg --decrypt [file name]
gpg --output [output name] --decrypt [file name]
```

Notes:
- Either command can be used
- Replace [file name] with the file containing your message
- Replace [output name] with the name of the file you want to contain the signed message (ending in `.txt`)

---

Further documentation available in *The GNU Privacy Handbook* online [here](https://www.gnupg.org/gph/en/manual.html).