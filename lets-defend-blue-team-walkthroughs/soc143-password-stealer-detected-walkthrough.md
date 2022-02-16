# SOC143 - Password Stealer Detected Alert

Hello readers, welcome to this blog entry as I document my journey through the world of Blue Teaming. Today, we will be trying our hand at the SOC143 — Password Stealer Detected alert, on the Let’s Defend platform.

## Introduction to the Case

The case particulars are given to analyze and understand:-

![](https://cdn-images-1.medium.com/max/1000/1\*0wZPA1nJXMuq1Txm30QHQw.png)

Next steps:-

> Take ownership of case

> Create Case

This case will be extra sweet to solve, as we get to analyze a phishing password stealer, that was used in a real-world cyberattack

> Start Playbook — a special component of investigation.Gives us a blueprint of steps to follow in a case,in an automated manner

## Playbook Questions

![](https://cdn-images-1.medium.com/max/1000/1\*J-nZRo10XtKD4FgGxtuBcQ.png)

Let’s have a look at our mailbox-for any information about the same. We were able to find this, a blank mail, with a single attachment.​

![](https://cdn-images-1.medium.com/max/1000/1\*BSGsYLxWXydLsGHqoUrsog.png)

Now, let’s download the attached file and unzip it, using the ‘unzip’ command and using the passphrase: infected

## Enumeration

We recover a file titled \[email protected]\_63963964Application.HTML, which is an HTML file. Now, viewing it on the browser, gives us the following webpage:-

![](https://cdn-images-1.medium.com/max/1000/1\*VWD7cwxxTG-Ibz-FYwNzJQ.png)

​At first glance, it looks like a Microsoft personalized phishing website designed to steal Ellie’s password, if she tries to login onto this page

Digging through the page source did not give us any red lights

## Playbook Questions

> Q) Are there attachments or URLs in the email? Please click “Yes” if there are an attachments or URLs in the email, if there are no attachments or URLs in the email please click “No”.

> Contains Attachment or Url?

> A) Yes

> Q) Analyze Url/Attachment in 3rd party sandboxes. Please click “Malicious” if it is malicious and click “Non-malicious” if it isn’t.

## A**nalysis of infected file**

We submit the HTML file for analysis on Virustotal and Hybrid-Analysis

First, over at Virus Total — 5 vendors classify the file as malicious​

![](https://cdn-images-1.medium.com/max/1000/1\*1z9vmwyX7MM-KT4D6Qr8uw.png)

​They classify the file as a part of a phishing attempt

Now onto Hybrid-Analysis

We find that the file has been run on two OS’ — Windows 7 (32 and 64 bit)-where both found the file to be malicious

![](https://cdn-images-1.medium.com/max/1000/1\*WiqTpy5CtfYPm8rK93en7A.png)

​So the file is indeed malicious&#x20;

> A) Malicious

> Q) Check If Mail Delivered to User? Answer the following question by determining whether the e-mail is delivered by looking at the “device action” part of the alert details.

Yes, we can find from the case particulars that device action has been set to allow

> A) Delivered

> Q) Check If Someone Opened the Malicious File/URL? Please go to the “Log Management” page and check if the c2 address accessed. You can check if the malicious file is run by searching the c2 addresses of the malicious file.

> Please click “Yes” if someone has accessed the malicious address. Otherwise please click “No” button.

We click yes&#x20;

> A) Yes

## Ad**ding artifacts to the casefile**

Now, it’s time to add a few artifacts to the case

Digging through more details, we find:-&#x20;

MD5 Hash of file — bd05664f01205fa90774f42468a8743a&#x20;

SHA — 1 Hash of file — f3df825ef2e3c70a5bc70f4a7c935be10a65bf57

This information was sourced from VirusTotal, under the ‘Details’ tab.

We add artifacts, that were collected during the enumeration process

![](https://cdn-images-1.medium.com/max/1000/1\*dHCuTZdYZ6ZMdevUwcLRHQ.png)

## F**urther Analysis of HTML File**

From the community section of VirusTotal, we find the Joe sandbox analysis of the same file​

![](https://cdn-images-1.medium.com/max/1000/1\*Sh-7zbLIJfV\_IMAAmQAOeA.png)

As an analyst, we conclude the case, by jotting some notes about the same

![](https://cdn-images-1.medium.com/max/1000/1\*0JtLYxjx2MMU3\_xlqUXt3w.png)

​Finish Playbook

Close Alert — by providing notes and classifying the alert, either as a true or false positive

![](https://cdn-images-1.medium.com/max/1000/1\*0uNcxWEjae2NVJ-rXiX7Yg.png)

## Alert Scorecard

![](https://cdn-images-1.medium.com/max/1000/1\*f8ALacksYVE641bmdxYmSQ.png)

20/25 points acquired. We got it wrong in one question. Further enumeration would have prevented us from committing that error

## **Summary of Alert**

A SOC Alert came in, asking us if a suspected phishing mail and its attachment was indeed malicious. Upon closer inspection, we found that it was designed to capture a user’s password, mimicking Microsoft’s Outlook login page, which is a classic example of a Phishing attack

## Conclusion

Thank you for devouring this blog entry and stay tuned as I try to close down more SOC alerts……

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed.Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
