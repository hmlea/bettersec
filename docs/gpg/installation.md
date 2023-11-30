---
layout: default
title: Installation
parent: GPG
nav_order: 1
---

# Homebrew

**[Homebrew](https://brew.sh/)** is an open source package manager for MacOS and Linux. Homebrew simplifies the installation of different packages by downloading and verifying them from a central source.

Homebrew is most easily installed via the command line. To install Homebrew, open up Terminal (easily done by pressing `⌘ + space` and searching for it) and copy the following command:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

This command downloads and installs the program off of GitHub and is the method recommended by Homebrew themselves. It may take some time to install. If installation fails, try adding `sudo` before the command above or troubleshoot and look into other installation methods [here](https://docs.brew.sh/Installation).

# Installing GPG

Now with a bit of an understanding of GPG, we can install it with Homebrew. We can install GPG with the following command:

```
brew install gnupg
```

After running, you can confirm it is installed with `gpg --version` which should bring up version details of the installed program.
