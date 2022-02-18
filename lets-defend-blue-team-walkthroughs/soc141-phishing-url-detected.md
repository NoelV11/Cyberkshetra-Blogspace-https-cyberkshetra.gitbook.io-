# SOC141 - Phishing URL Detected

Hey blue teamers, hope you are hale and hearty!

This is yet another blog entry, where we will be focusing on solving Let’s Defend’s SOC141 — Phishing URL Detected alert

Spoiler alert: There is something awesome being mentioned at the end of this article, so hang tight!

## Introduction to the Alert

We are given the alert details to understand. By going through it, we can determine that this is a classic phishing attack attempt

&#x20;                                                     ![](https://cdn-images-1.medium.com/max/1000/1\*-E9m1imob2W4hCTMx8YewA.png)

> Take ownership of the case\
> Proceed to create the case

Start the playbook

&#x20;                                                     ![](https://cdn-images-1.medium.com/max/1000/1\*fh6ANtxb02gq3clTk4wKfw.png)

## Collection of Data

Below, we are given a few details to source. The required information is specified in the alert summary

&#x20;                                                        ![](https://cdn-images-1.medium.com/max/1000/1\*BYlH1v1SDtQbonmNKj2t-A.png)

> Source Address — 172.16.17.49\
> Destination Address — 91.189.114.8\
> User-Agent — Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36

## Search Log

&#x20;                                                      ![](https://cdn-images-1.medium.com/max/1000/1\*8y9siGUYkpwC-r4Z1Jln4A.png)

Now checking Log Management

We try to filter out existing network logs, by entering the source and destination IP’s as input. The resulting two entries show some data being accessed from the victim host

![](https://cdn-images-1.medium.com/max/1000/1\*aJ55u6shGtNdoPVUXEvmLQ.png)            ![](https://cdn-images-1.medium.com/max/750/1\*cmzBRPqYfLKvAMHw2ss2BA.png)

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*3h7heP\_IfmMmNGZiiJxqZw.png)

## Analyze URL Address&#x20;

&#x20;                                               ![](https://cdn-images-1.medium.com/max/1000/1\*SBOR1ZUo1lVkaocUfw9GjA.png)

Domain for analysis — [http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend.io](http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend.io)

To fulfill my curiosity, I decided to visit this domain&#x20;

**Remember to analyze alerts on a VM**

We find that the domain is hosted on WordPress and seems to be a dead-end

&#x20;                                            ![](https://cdn-images-1.medium.com/max/1000/1\*1-qYspTQJrb4vyPfcJLBRA.png)

### Domain Analysis

Let’s submit this domain, to [Virustotal.](https://www.virustotal.com/gui/home/upload) It will determine whether the site is malicious or not

Turns out, the site was indeed malicious and is classified as a phishing domain

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*nvfKfTbuKtshihcr15HIqA.png)

Virustotal analysis of domain (mogagrocol.ru)

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*APvV8U3llauyKILhUYCRVA.png)

This domain is classified under the ‘Phishing’ domain

&#x20;                                                    ![](https://cdn-images-1.medium.com/max/1000/1\*XDeiB6Tst3WXxGYuipThAg.png)

So we select — Malicious

> A)Malicious

## Has Anyone Accessed IP/URL/Domain?

&#x20;                                               ![](https://cdn-images-1.medium.com/max/1000/1\*0paPNTFmtnQhsfZ0DbVHEA.png)

Accessing Log Management and viewing logs from both Source and Destination IP’s

&#x20;             ![](https://cdn-images-1.medium.com/max/750/1\*cmzBRPqYfLKvAMHw2ss2BA.png)![](https://cdn-images-1.medium.com/max/1000/1\*3h7heP\_IfmMmNGZiiJxqZw.png)

When verifying against contacted hosts — Image 11 and 10(1)

![](https://cdn-images-1.medium.com/max/1000/1\*ghjcNejcsnBkLPL2DSE8rQ.png)![](https://cdn-images-1.medium.com/max/750/1\*DNLSKDu0LlL4J2Lgpu-XCw.png)

&#x20;                                  ![](https://cdn-images-1.medium.com/max/1000/1\*6R4t58RACvSWSWReV7qURA.png)

We can find that the host hasn't contacted the malicious domain — from the ‘Contacted Hosts’ history, from [Hybrid-Analysis](https://www.hybrid-analysis.com)

Answering the questions from above:-

> A)Mar, 22, 2021, 09:23 PM

> A)172.16.17.49

> A)91.189.114.8

> A)ellie

> A)Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36

> A)Allowed

In retrospect, I was initially confused whether the host had accessed the phishing domain and decided to go against it. Hence I selected ‘No’

**From the evidence above, it is evident that the victim had accessed the domain**. This is an honest write-up after all.No cheating or cutting corners!

I wouldn't want you to make the same mistake

We select ‘Not accessed’

> A)Not accessed

## Add Artifacts

To hunt down any mail addresses associated with this phishing domain, I used Maltego to trace out every information it had, related to the site

Safe to say, it did not fail us, but I was unable to glean any useful information

&#x20;                                           ![](https://cdn-images-1.medium.com/max/1000/1\*iWRzt3dUnD-qs9p5N8IBaw.png)

However, we have a few IPs, outgoing links, and a malicious domain to submit as case artifacts!

&#x20;          ![](https://cdn-images-1.medium.com/max/1000/1\*aAAxGI4\_2D5Y6Clv3WdhTw.png)![](https://cdn-images-1.medium.com/max/750/1\*IQApi5Y3g9qTLKaMIj-rwQ.png)&#x20;

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*9btivc7cxKs6Sc9gbGS68Q.png)

Click on next to submit the artifacts

Finish the playbook and close the alert

## Parting Notes

We proceed to add a few notes, before closing the case. List every incident in a crisp manner

&#x20;                                                 ![](https://cdn-images-1.medium.com/max/1000/1\*7SpGPAl26GP5Lk5cWFFpJg.png)

## Alert Scorecard

This is not a bad score at all, but I wish I had been a bit more careful, in getting the wrong answer right. Every alert solved is a step towards perfection and I am pretty happy with the score I received

&#x20;                                                    ![](https://cdn-images-1.medium.com/max/1000/1\*lguLifzdPkCtQz1efm8a2A.png)

## A perfect ending

Upon submitting my answers, I was met with this beauty of a badge.It looks pretty awesome and I am proud of myself, for having achieved it!

I would encourage you to give Let’s Defend a try and see how you enjoy and learn from it!

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*GbWIJou7K5iQWVhyXdqjHQ.png)

## Summary of the alert

A phishing mail was sent to a host, on the Let’s Defend network (EmilyComp). From the network logs, it was found that the victim host had accessed the phishing domain.

Running the domain on VirusTotal confirmed our suspicions and to close the case, important artifacts were collected and submitted

The case was a true positive for a phishing attack and the analyst responsibly provided artifacts and notes, discussing the case characteristics and results

## Conclusion

Thank you for reading this blog entry, and stay tuned as I try to close down more SOC alerts……

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
