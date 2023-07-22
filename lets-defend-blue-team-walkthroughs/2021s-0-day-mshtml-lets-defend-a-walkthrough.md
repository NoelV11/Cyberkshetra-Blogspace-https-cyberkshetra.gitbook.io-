---
description: CVE-2021–40444 Lab
---

# 2021’s 0-Day MSHTML: Let's Defend Lab

![](<../.gitbook/assets/1 (7).png>)

Hello, budding blue teamers.Welcome to this latest blog entry, where I will be wading deep into the 'Malware Analysis' path on Let's Defend and attempting to solve the [2021’s 0-Day MSHTML](https://app.letsdefend.io/malwareanalysis/analysis/mshtml/) lab.

Challenge credits go to [Bohan Zhang](https://www.linkedin.com/in/bohan-zhang-078751137/) and malware sample provision by [MalwareBazaar](https://bazaar.abuse.ch/)

Let's analyze some malware!

**NOTE: Always remember to investigate challenges from Let's Defend, on a VM.**

## Introduction

We are given a 'Challenge' file to analyze. Proceed to download the file

Unzip the file, with password: infected

Upon unzipping, we get a directory called ‘Challenge\_FIles’, with 4 files

![](https://cdn-images-1.medium.com/max/1000/1\*tUSRyN1oH25P0-Ali9WHJw.png)

## Challenge Questions

> Q) Examining the Employees\_Contact\_Audit\_Oct\_2021.docx file, what is the malicious IP in the docx file?

Targetting the ‘Employees\_Contact\_Audit\_Oct\_2021.docx’ file, let's run a strings search over it

`Command — strings Employees_Contact_Audit_Oct_2021.docx`

Unable to find any IP’s from the resulting output, the next resort would be to use the [Hybrid-Analysis ](https://www.hybrid-analysis.com/)tool

After uploading the file to be analyzed, we can see its malicious level on test sandboxes

![](https://cdn-images-1.medium.com/max/1000/1\*m\_rFKA-ARXoU\_q45pzUjtA.png)

Scrolling down, we proceed to check extracted strings from the file 

![](https://cdn-images-1.medium.com/max/1000/1\*zHYBVxFtiSHO1ZM7A7pHmQ.png)

We can see an IP mentioned here — 175.24.190.249

Scrolling up, we can see the connection traffic from this IP

![](https://cdn-images-1.medium.com/max/1000/1\*qyLNNKOmohyzd\_x0a78F7g.png)

Since this is the only IP extracted from the malware file, coupled with its suspicious traffic traces, we can confirm this as the answer

> A) 175.24.190.249

> Q) Examining the Employee\_W2\_Form.docx file, what is the malicious domain in the docx file?

Running a strings analysis over this file did not reveal the malicious domain that we needed

Uploading this file onto Hybrid-Analysis, we get to see its malicious level

![](https://cdn-images-1.medium.com/max/1000/1\*\_ua-FRuDZw3ycPaGacg9Tw.png)

Now observing extracted strings from this file 

![](https://cdn-images-1.medium.com/max/1000/1\*Ps4LREw9O3z1X7zc-OjEjQ.png)

A domain by the name arsenal.30cm.tw is found and fits the answer format

> A) arsenal.30cm.tw

> Q) Examining the Work\_From\_Home\_Survey.doc file, what is the malicious domain in the doc file?

Running the Work\_From\_Home\_Survey.doc file on Hybrid-Analysis

The severity of malicious content is shown below

![](https://cdn-images-1.medium.com/max/1000/1\*1Kt8vuQoWxFmXrrMHj\_1YA.png)

Reading through the metadata of the file, we can see that the file supposedly contacts a domain

![](https://cdn-images-1.medium.com/max/1000/1\*GrNE8pqQ\_rV5ngCLRJp0xw.png)

Clicking on ‘View all details’

![](https://cdn-images-1.medium.com/max/1000/1\*rI8YE5YnfLcCDl1Xla28VQ.png)

A domain named ‘trendparlye.com’ pops up here\
Opening [AlienVault](https://otx.alienvault.com/)’s assessment on this domain gives us the following information

![](https://cdn-images-1.medium.com/max/1000/1\*MoM33HV7ggOtZOufybcWmQ.png)

This means that the domain is malicious

> A) trendparlye.com

> Q) Examining the income\_tax\_and\_benefit\_return\_2021.docx, what is the malicious domain in the docx file?

We proceed to run the income\_tax\_and\_benefit\_return\_2021.docx file on the Hybrid-Analysis tool

Malicious severity of file can be observed below:-

![](https://cdn-images-1.medium.com/max/1000/1\*EPmZ5J8sAjz0nrZvCB8WzA.png)

Having a look at the extracted strings section, this file has contacted an external domain too.

Let’s check the domain out - 'hidusi.com'

![](https://cdn-images-1.medium.com/max/1000/1\*qJz5W4RljH3HFN0xBKD9Jw.png)

Looking up the domain on AlienVault 

![](https://cdn-images-1.medium.com/max/1000/1\*qa-4VQlcmVS-0aSL6LLr-A.png)

> A) hidusi.com

> Q) What is the vulnerability the above files exploited?

Throughout the analysis of each suspicious file, I had been collecting their SHA-256 hashes, which are listed below:-

> (Employees\_Contact\_Audit\_Oct\_2021.docx)
>
> SHA 256 Hash — 8aaa79ee4a81d02e1023a03aee62a47162a9ff04

> (Employee\_W2\_Form.docx file)
>
> SHA 256 Hash — 00087e46ec0ef6225de59868fd016bd9dd77fa3c

> (income\_tax\_and\_benefit\_return\_2021.docx)
>
> SHA 256 Hash — 9bec2182cc5b41fe8783bb7ab6e577bac5c19f04

> (Work\_From\_Home\_Survey.doc)
>
> SHA 256 Hash — 4b35d14a2eab2b3a7e0b40b71955cdd36e06b4b9

Running any of these hashes on [VirusTotal](https://www.virustotal.com/gui/home/upload) and checking out the ‘Community’ section gives us the answer that we are dealing with the CVE-2021–40444 known as MSHTML RCE Vulnerability (if it was not already obvious from the title of this challenge!)

Let’s take the help of the hint, to find the answer format

> A) CVE-2021–40444

## Conclusion

Lookups of real-world malware samples made me enjoy the time spent practicing this room. This will be an almost daily occurrence when eventually stepping into the shoes of a SOC Analyst, which I aspire to be

Thank you for devouring this blog entry and stay tuned as I try to close down more SOC alerts……

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
