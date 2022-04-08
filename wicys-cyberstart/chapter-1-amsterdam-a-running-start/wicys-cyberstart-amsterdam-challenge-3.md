---
description: Web-login bruteforce
---

# WiCYS CyberStart (Amsterdam) Challenge 3

![](../../.gitbook/assets/CS.png)

## Briefing L01 C03

### Social Engineering

![](<../../.gitbook/assets/1 (3).png>)

> Permission has been granted to try and log into the Chirp social media account of a hacker who goes by the name of D4YDR3AM. Luckily for us. they’ve been clumsy with their personal information. We know their dog’s name is Barkley and they were born in 1993. Can you use what we know about them to guess their password and get us into their account?

> **Tip**: Get the flag by guessing the correct password to sign into the account.

Let's go to the challenge

We are met with this Chirp login page (mimicking Twitter again!)&#x20;

![](<../../.gitbook/assets/2 (2).png>)

I guess we won't have to think hard to crack this, unless it involves creating a wordlist using [crunch ](https://www.irongeek.com/i.php?page=backtrack-r1-man-pages/crunch)(to generate passwords) and using it to bruteforce the login page, using [Hydra](https://www.mankier.com/1/hydra) or [Burp Suite](https://www.pluralsight.com/paths/web-security-testing-with-burp-suite#:\~:text=Burp%20Suite%20is%20an%20integrated%20platform%2Fgraphical%20tool%20for%20performing,finding%20and%20exploiting%20security%20vulnerabilities.)

I had these three combinations in mind:-&#x20;

> Barkley1993

> Barkley93 and

> 1993Barkley

## Flag Capture

Let's go ahead and bruteforce em'

The first password worked in this case and we have logged in.

First time lucky eh?

![](<../../.gitbook/assets/3 (3).png>)

We get the flag and submit it

> _Flag — F3Fhrc07TPmJ2HZAY9cd_

### Scoreboard

![](<../../.gitbook/assets/screenshot (2).png>)

There’s no looking back. Onward ahoy!

![](<../../.gitbook/assets/4 (2) (1).png>)
