---
description: Powershell-fuelled malware
---

# SOC137 — Malicious File/Script Download Attempt: A Walkthrough

Welcome blue teamers!

Now, who is ready to do some SOC alert practice? Today I will be guiding you through the SOC 137 (Malicious File/Script Download Attempt) alert.

**NOTE: Always remember to investigate alerts from Let’s Defend, on a VM.**

## Introduction to the Alert

Preceding the investigation, we are given a rundown of the alert summary. It contains vital information that comes in handy later

&#x20;                                               ![](https://cdn-images-1.medium.com/max/1000/1\*6klosU4pzAwOt5rCvTkHKw.jpeg)

> Take ownership

> Create case

Start Playbook

&#x20;                                                 ![](https://cdn-images-1.medium.com/max/1000/1\*G5J302MdjI9zf4YXSHQZnQ.jpeg)

Now, let’s delve into the questions

## Define Threat Indicator

Select Threat Indicator

&#x20;                                                 ![](https://cdn-images-1.medium.com/max/1000/1\*uCQzCoyLo5erG80gR4nSeQ.jpeg)

From the alert summary, we can find that the malicious .zip file was downloaded onto the NicolasPRD endpoint, with IP Address — 172.16.17.37

Upon unzipping it, we uncover a file named ‘INVOICE PACKAGE LINK TO DOWNLOAD.docm’

### Enumeration and Analysis

Applying Linux’s file command, we determine that the version of Microsoft Word used is from 2007

&#x20;                                                    ![](https://cdn-images-1.medium.com/max/1000/1\*4dMsxQOoXy4Z7S9S3grrrA.jpeg)

It would be wise to give the malicious file a run on [Anyrun](https://any.run/). It is much safer that way.\
Upon uploading, we find its contents below

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*oZCJwFpYXYDfhc0FsPowxA.jpeg)

Process breakdown&#x20;

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*sOxKG0sprVC\_\_XMZp80wZw.jpeg)

From the process tree of the malicious file, we can see that it has a PowerShell executable as a subprocess. The executable is given read permissions, which can be fatal, if not monitored properly.

This becomes evident especially when it has a 95% severity rate of being suspicious

### Analysis using VirusTotal&#x20;

&#x20;                                                    ![](https://cdn-images-1.medium.com/max/1000/1\*HGJyCU8negRdXVDBnNp8pQ.jpeg)

### Analysis using VirusTotal&#x20;

Making use of [Hybrid-Analysis](https://www.hybrid-analysis.com/), we have received conclusive evidence of the file being malicious. Malicious and Suspicious IOCs have been identified and displayed below&#x20;

![](https://cdn-images-1.medium.com/max/1000/1\*uIptW7rD\_wYKDMEm8BrsBg.jpeg)![](https://cdn-images-1.medium.com/max/750/1\*Rm9qwo5K5GcuWF43b7520g.jpeg)

Judging from the evidence and characteristics of the malicious file collected above, we can conclude that the file contacts external domains, through undetected outgoing network traffic

> A)Unknown or unexpected outgoing internet traffic

&#x20;                                                  ![](https://cdn-images-1.medium.com/max/1000/1\*bavFvU0le-SAzKCqvNZ38A.jpeg)

## Check if the malware is quarantined/cleaned

&#x20;                                                    ![](https://cdn-images-1.medium.com/max/1000/1\*c\_wEDuD-YCkVDrNAZBAKCQ.jpeg)

I believe that the malware hasn't been quarantined

> A)Not Quarrantined

## Analyze Malware

&#x20;                                                        ![](https://cdn-images-1.medium.com/max/1000/1\*orj2w4wpSeQgEwiO1tA-yw.jpeg)

> Analyze malware in 3rd party tools and find C2 address

> You can use the free products/services below.

> AnyRun\
> VirusTotal\
> URLHouse\
> URLScan\
> HybridAnalysis

From our analysis, we have concluded that the file is indeed malicious

> A)Malicious

## Check If Someone Requested the C2

&#x20;                                                         ![](https://cdn-images-1.medium.com/max/1000/1\*RaEhJ2GX6gRdJNWez7oABQ.jpeg)

> Please go to the “Log Management” page and check if the C2 address accessed. You can check if the malicious file is run by searching the C2 addresses of the malicious file.

> Log Management\
> Please click “Yes” if someone access the malicious address. Otherwise please click “No” button.

Let’s look up the source IP Address (172.16.17.37) on the Log Management section

We get 3 corresponding log entries, but none of them relate to the alert or show any reference to the download of a malicious file (as briefed to us)

&#x20;                                                      ![](https://cdn-images-1.medium.com/max/1000/1\*klchgR\_yhs2dJyDYbu0EUg.jpeg)

Using Hybrid-Analysis to pull up the list of contacted hosts, we find the following domains and IP addresses to verify with

&#x20;                                                       ![](https://cdn-images-1.medium.com/max/1000/1\*Npi4hiibTIjwoztSag7U3A.jpeg)

None of the IP Addresses match. Hence we can assume that the C2 Server was not contacted. What are we doing wrong here?

Now, for further verification let’s use the Relations tab of VirusTotal (corresponding to the malicious file)

We finally strike gold here.

&#x20;                                                         ![](https://cdn-images-1.medium.com/max/1000/1\*ISvMZiQXMQ4Zh-vdKHhxzA.jpeg)

172.67.200.96 can be labeled as the IP Address of the C2 Server and it has been accessed by the NicolasPRD endpoint (victim host)

> A)Accessed

## Containment

&#x20;                                                           ![](https://cdn-images-1.medium.com/max/1000/1\*IGw2wU6D3EegJvUaPMhQgA.jpeg)

> Please go to the “EDR” page and contain the user machine!

> Endpoint Security\
> After containment please click “Next” buttton to finish playbook.

Proceed to contain the NicolasPRD endpoint

&#x20;                                                         ![](https://cdn-images-1.medium.com/max/1000/1\*AslvHnbHCwPpRgFSf6xkwg.jpeg)

### Add Artifacts

We have identified the domains contacted by the malicious file, as well as its MD5 hash, from VirusTotal

&#x20;                                                        ![](https://cdn-images-1.medium.com/max/1000/1\*2dvNyS38U6DGbL1lpodJ9A.jpeg)

We proceed to compile this into our Artifacts chart

![](https://cdn-images-1.medium.com/max/750/1\*se2EDz7Fzci48G\_6HV1AdQ.jpeg)![](https://cdn-images-1.medium.com/max/1000/1\*ygQ92zuZ02Evt\_j-EIL8Wg.jpeg)

## Analyst Note

Detail this section as much as you can. A good SOC Analyst gives attention to detail.

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*d9tT2jt4Dg\_0DxmJZoWO6w.jpeg)

> Finish the playbook\
> Close the alert

## Alert Scorecard

&#x20;                                                  ![](https://cdn-images-1.medium.com/max/1000/1\*IUeCNdag\_jyCcOQ53FHImw.jpeg)

Ok, that was unexpected.

Every alert solved is a step towards perfection and I am pretty happy with the score I received.

## Summary of the alert

The SOC Analyst was given a zip file, from which a .docm file containing a suspicious link was extracted. This file was subsequently detected and was found to be malicious.IOCs relating to the file, along with contacted hosts were collected, culminating in the containment of the NicolasPRD endpoint (victim host)

## Conclusion

Thank you for reading this blog entry, and stay tuned as I try to close down more SOC alerts……

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
