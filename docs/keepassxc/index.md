---
layout: default
title: KeePassXC
nav_order: 3
has_children: true
permalink: /docs/keepassxc
---

# Overview

KeePassXC is a free open-source, self-hosted password manager. KeePassXC is actively developed and used by many, allowing it to stay ahead and quickly patch newly revealed vulnerabilities. KeePassXC runs on all computer operating systems and utilizes a universal database that can be opened on other mobile systems such as iOS. Additionally, KeePassXC is extremely transparent with its security and has been externally audited as recently as January 2023 (read more [here](https://keepassxc.org/docs/#faq-audit)).

Unlike many popular password managers that are often advertised on TV and on billboards, KeePassXC is self-hosted. This means that your database is stored locally on your machines instead of in the *cloud* like other providers do. Put simply, the cloud is just another random person's computer that is online for you to conveniently access your data. This brings rise to two large problems: 1) you aren't actively in posession of your data but instead, some other person you don't know has it, and 2) hosting your database online introduces many new routes for attackers to steal your passwords. These two problems have been proven to be detrimental as time and time again we have seen large scale hacks such as the recent [LastPass hack](https://www.forbes.com/sites/daveywinder/2022/08/25/lastpass-hacked-password-manager-with-25-million-users-confirms-breach/?sh=6fb70a2b7d5a) in August of 2022.

"But why do I need a password manager at all? I remember all my passwords!" In 2023, using even relatively short, common, or repeated passwords doesn't cut it anymore. In an ideal world, you would have long, random, and complex passwords for each service with no two passwords being similar in any manner. The reality is this is not feasible to do or remember without a password manager.

The chances are that your password/information has been leaked before in a data breach; you can check this at [haveibeenpwned.com](https://haveibeenpwned.com/). And while this site is ethical and doesn't offer to sell the data breaches, you don't have to look far to find a site who will. Even if your data hasn't been breached, if your password is not random, it is likely extremely easy for an attacker to crack your password using modern methods such as complex [rainbow tables](https://en.wikipedia.org/wiki/Rainbow_table), [dictionary attacks](https://en.wikipedia.org/wiki/Dictionary_attack), or pure [brute force](https://en.wikipedia.org/wiki/Brute-force_attack).

The solution to this is to use a password manager, where you only have to remember one exceptionally strong password instead of hundreds. KeePassXC is not only advantageous in the fact that it is self-hosted and stored offline, but also lets you generate entropically strong passwords that are resistant to attack and store other files and information in your database as well.

---

Read more about KeePassXC in their documentation [here](https://keepassxc.org/docs/).