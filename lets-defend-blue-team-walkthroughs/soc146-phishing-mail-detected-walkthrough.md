# SOC146 - Phishing Mail Detected  Walkthrough

Welcome to my blue teaming journey, as I tackle my second case: (SOC146 — Phishing Mail Detected — Excel 4.0 Macros) on the LetsDefend platform, which is of Medium difficulty

### Introduction to Case

Let’s have a look at the case details:-

![](https://cdn-images-1.medium.com/max/1000/1\*rf5NUnFR6Ji0-mhMhvSKrQ.png)

Next, we have a look through our Letsdefend Mailbox, to find any information. Searching with the keyword ‘Trenton’ gives us:-​

![](https://cdn-images-1.medium.com/max/1000/1\*B3cRVYSUY-fA1aw-fRPGCA.png)

We download the file onto the machine and unzip it, using the keyphrase: infected

Now,we have a directory titled — 11f44531fb088d31307d87b01e8eabff

### Viewing File Contents

Opening the directory gives us 3 files (2 .dll and a .xls file).We analyze the .xls file, which we open online.Its contents are:-

![](https://cdn-images-1.medium.com/max/1000/1\*VPeDJ-4OqpaFOEH42psOvg.png)

### Analysis on VirusTotal and Hybrid-Analysis

Next, we run the 3 files on Hybrid Analysis and VirusTotal tools

The Hybrid- Analysis tool gives us an overview of the malicious content of the submitted files

![](https://cdn-images-1.medium.com/max/1250/1\*nMQ6niOzrnomxPnGYd7o3A.png)

![](https://cdn-images-1.medium.com/max/500/1\*O9YAPdHnUB4C7d6dwpRQTg.png)

iroto.dll — 7/68 security vendors flag it as malicious

(Hash — 07d83e3cbda0ddafb93dd8b6bd3d94fdd96797242d52b4b818a5d85f82b95be0)

iroto1.dll — 8/66 security vendors flag it as malicious

(Hash — e05c717b43f7e204f315eb8c298f9715791385516335acd8f20ec9e26c3e9b0b)

research-1646684671.xls — 30/59 security vendors flag it as malicious

(Hash -1df68d55968bb9d2db4d0d18155188a03a442850ff543c8595166ac6987df820)  

\=====================================================================

Lets Defend Questions:-

Step 1  - Are there any attachments or URL’s within the email — Yes

Step 2 - Are the files malicious? — Yes

(Answers gained from initial enumeration)

\=====================================================================

Step 3 - Check if mail is delivered to the user? (Hint: look at the “device action” part of the alert details)

Here, the receiver is \[email protected] Checking the Device Action, it says “Allowed” — probably means that the mail was in fact delivered to the intended user ••

\=====================================================================

Step 4&#x20;

Q)Check If Someone Opened the Malicious File/URL? (Hint: Please go to the “Log Management” page and check if the c2 address was accessed. You can check if the malicious file is run by searching the c2 addresses of the malicious file.)

We scroll down to extracted strings and other information, from the .xls file on the Hybrid-analysis tool

Hybrid-analysis shows us that there are a few extracted files from the .xls file, namely:-

> index.dat research-1646684671.LNK 103621DE9CD5414CC2538780B4B75751 57C8EDB95DF3F0AD4EE2DC2B8CFD4157 644B8874112055B5E195ECB0E8F243A4 E27E358D5143FC43BA3563902E94BBBD

These files run as excel.exe on the target machine

Enumerating more, we find that IP 188.213.19.81(originating from Romania) has accessed this, resulting in some bad traffic.

Also, IP Address— 192.232.219.67 (originating from USA) has accessed it as well

These two users have fallen victim to a phishing attack, downloading and accessing malicious files along the way

![](https://cdn-images-1.medium.com/max/1000/1\*CeeWhwSiXvzIx5g0Luzp-w.png)

Now running the acquired IP Addresses on Letsdefend’s log management section, we find hits for both:-

![](https://cdn-images-1.medium.com/max/1000/1\*eHO1bYgNNUBrXC66N7mpEg.png)

### Detailed Overview of the Log Management entry

![](https://cdn-images-1.medium.com/max/1000/1\*nj56s\_dGLj\_bYcfgxfqgTA.png)

So it means that the infected files have been accessed and the malicious excel.exe file is running as process id 3816 on infected hosts

Now we add a few artifacts that were collected during the investigation (IP Addresses and extracted files from the .xls file)

![](https://cdn-images-1.medium.com/max/1000/1\*EXb5NRGLwPInC7lk9ve6NQ.png)

### Adding Analyst's notes

![](https://cdn-images-1.medium.com/max/500/1\*h9l9\_l\_nHkHaRpmWJh2qpg.png)

![](https://cdn-images-1.medium.com/max/1000/1\*K6yBwYqCl3R2HiRpge-hhQ.png)

Now, we close the alert — classifying the event as a true positive

True Positive (+5 Points)

Check If Someone Opened the Malicious File/URL? (+5 Points)

Check If Mail Delivered to User? (+5 Points)

Analyze Url/Attachment (+5 Points)

Are there attachments or URLs in the email? (+5 Points)

**==================================================================**

### Alert Score Card

![](https://cdn-images-1.medium.com/max/1000/1\*LRG0wt1N5Upg7Na55J8uyg.png)

This case was fascinating and I was double happy with the fact that I got all answers right!

### Summary of Case

A phishing mail was sent from source 172.16.17.57, disguised as a harmless document, which led to two users falling for the attack, downloading the mail’s malicious content. A total of 3 files were recovered and analyzed, having malicious characteristics.

The case was a true positive for a phishing attack and the analyst responsibly provided artifacts and notes, discussing the case characteristics and results

Thank you for reading this blog entry. Stay tuned, as I go hunting some pcap files out there….
