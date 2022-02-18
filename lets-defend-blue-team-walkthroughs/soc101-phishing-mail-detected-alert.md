# SOC101  -  Phishing Mail Detected Alert

Hello, blue teamers. In this blog entry, join me as I attempt to conquer the SOC 101 — Phishing Mail Detected alert, hosted on[ Let’s Defend](https://letsdefend.io).

**NOTE: Always remember to investigate alerts from Let's Defend, on a VM.**

## Introduction to the Alert

Let’s have a good look at the alert, to familiarize ourselves with the details

&#x20;                                           ![](https://cdn-images-1.medium.com/max/1000/1\*KqlRkaOm5oVsrkOPFNE2Pw.png)

> Proceed to take ownership of the case\
> Create case

## Initial enumeration

Since the SOC alert deals with phishing mail, let’s have a look at Let’s Defend’s mailbox, titled ‘Exchange’, and search by the mail address of the victim — [mark@letsdefend.io](mailto:mark@letsdefend.io)

This is the sent mail in question:-

&#x20;                                               ![](https://cdn-images-1.medium.com/max/1000/1\*FuOAk\_aB85QiAfR05uVRQA.png)

We’ve got our first bit of evidence here, a malicious domain — [http://nuangaybantiep.xyz](http://nuangaybantiep.xyz)

Seems like an email was sent to Mark’s Phone. It’s not a desktop endpoint that we are looking for here

Checking the ‘Endpoint Security’ section, we come across Mark’s phone, titled ‘MarksPhone’&#x20;

&#x20;                                               ![](https://cdn-images-1.medium.com/max/1000/1\*mEKTfcSzI6vXh1RjJzrucQ.png)

## Incident details&#x20;

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*thV-8FOIpMRccpX7s6W8Ew.png)

Let’s proceed to start the playbook

## Playbook Questions

### Parsing the email

&#x20;                                                 ![](https://cdn-images-1.medium.com/max/1000/1\*RrpxJe7xOaa0JU2\_4k8yfA.png)

\
These answers are visible from our alert summary:-

> A1) April 4, 2021, 11 p.m.\
> A2) 146.56.195.192\
> A3) [lethuyan852@gmail.com](mailto:lethuyan852@gmail.com)\
> A4) [mark@letsdefend.io](mailto:mark@letsdefend.io)\
> A6) No

Is the content malicious?

To check it, let’s run the given domain ([http://nuangaybantiep.xyz](http://nuangaybantiep.xyz)) on a few threat intel platforms namely VirusTotal and Hybrid-Analysis, and Joe sand Box

While the former two returned clean checks on the domain, Joe Sandbox had something else to say, which can be seen below:-

&#x20;                                            ![](https://cdn-images-1.medium.com/max/1000/1\*mnA07tmYEmUJnxhmxbeDjg.png)

\
The site was definitely suspicious, but had no malware configuration evidence attached to it&#x20;

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*33fs072\_3B76w8g7SIJ-Ng.png)

> A) Non-suspicious

### Attachments or URLs in the mail?

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*Vut6kvw370bCTqKc9g7F0g.png)

> A) Yes

### Analyze Url/Attachment

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*xjhkXiMQEx2kAgPI5UaahA.png)

From JoeSandbox we understand that the domain was earlier used to spread trojan, but is now unreachable to us and is not causing any harm.

&#x20;                                            ![](https://cdn-images-1.medium.com/max/1000/1\*i-WvTue4wCa\_AcDn-oKoOA.png)

Analysis of the domain, from VirusTotal and Hybrid-Analysis, is testament to that

&#x20;         ![](https://cdn-images-1.medium.com/max/1500/1\*HfOuqTAagMuyaPsDcjDtmg.png)![](https://cdn-images-1.medium.com/max/250/1\*yM0kuoGA7vwaXBTf9yPUEA.png)

Hence, the domain is non-malicious

> A) Non-malicious

## Adding artifacts

Let’s fill in the table, with the evidence and related information, collected so far

&#x20;                                         ![](https://cdn-images-1.medium.com/max/1000/1\*nbjG2GephmMBwTrQvUiMSw.png)

From VirusTotal, we can get information about the serving IP Address and final domain destination, from the suspected domain

&#x20;                                             ![](https://cdn-images-1.medium.com/max/1000/1\*U4HaIgLxZrUGe3KsNZF3Iw.png)

Click next, to submit them

## Analyst's Notes

This is the analyst’s opinion on the alert

&#x20;                                               ![](https://cdn-images-1.medium.com/max/1000/1\*uIiryO1dZQx1QbrR\_NdBgQ.png)

Finish the playbook

Close the alert

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*NYENEYtcUx-f52bnqCAzRw.png)

## Parting notes

&#x20;                                             ![](https://cdn-images-1.medium.com/max/1000/1\*EjSRnc1CqEUQY78EeAJt9g.png)

## Alert Scorecard

&#x20;                                            ![](https://cdn-images-1.medium.com/max/1000/1\*zaOyL6cM6BRJ8p6MB-tvCQ.png)

We were not able to achieve the objectives required to completely solve this alert. Let’s take it as a learning opportunity, to go ahead and crush other incoming SOC alerts!

Every alert solved is a step towards perfection and I am pretty happy with the score I received.

## S**ummary of the alert**

A phishing mail has come in, to one of Let's Defend's endpoints. Upon investigation, it was found that the link attached was malicious in nature. It had been used to peddle malware in the past and it is understood that the endpoint user did in fact click on the link.&#x20;

All relevant evidence and information has been collected and submitted, confirming the alert as a true positive&#x20;

## Conclusion

Thank you for reading this blog entry. Stay tuned, as I go hunting behind some pcap files out there....

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by giving it a clap!
