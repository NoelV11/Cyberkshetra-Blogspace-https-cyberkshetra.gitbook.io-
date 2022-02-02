# Let’s Defend: SOC 142 — Multiple HTTP 500 Response alert Walkthrough

It’s the first week of February and that just means one thing. Let’s Defend has released a new set of SOC Alerts for us blue teamers to investigate and solve and here, we will be solving the SOC 142 — Multiple HTTP 500 Response alert.

Let’s jump right into it!

## Alert Details

![](https://cdn-images-1.medium.com/max/1000/1\*Ols\_9PA7exPTgtv22bHXwg.png)

Let’s take ownership of the case

Reading the alert’s summary and the payload, it’s plain to see that a SQL Injection was attempted on the target host

We must understand that web code 500 is an Internal Server error, which means the webserver on the client-side is not able to process the request

Create a case book for the same

![](https://cdn-images-1.medium.com/max/1000/1\*tN5r27Ik0Xz-wrhEk1CGLQ.png)

\
Start Playbook

![](https://cdn-images-1.medium.com/max/1000/1\*FdiCriAJMGWRj0KIEd\_rdQ.png)

## Collection of Data

> Q)Please check alert details for the following below:-

> Source Address\
> &#x20;Destination Address\
> &#x20;User-Agent

From the alert, we can determine

> A)Source Address — 172.16.17.88\
> Destination Address — 192.64.119.190\
> User-Agent — Mozilla — Windows

Let’s proceed to the next screen, where we find:-

![](https://cdn-images-1.medium.com/max/1000/1\*P\_EdaqCEANMqP\_s7A52ITA.png)

## Search Log

> Q)Please search in Log Management for details.

> Log Management

Searching the ‘Log Management’ section — we come across seven log entries&#x20;

![](https://cdn-images-1.medium.com/max/1000/1\*Uv1-lrufvh5HVB4JYxdb3A.png)

Expanding the first log, we get,

![](https://cdn-images-1.medium.com/max/1000/1\*9DEkzhMUcqAe9jF3rQ9L3Q.png)

\
Expanding the second log, we get,\
\


![](https://cdn-images-1.medium.com/max/1000/1\*vKuqfmtebfK6U\_gizatlEA.png)

Expanding the second log, we get,

![](https://cdn-images-1.medium.com/max/1000/1\*0JUbsyPNdbqHJsNp0kiM8A.png)

It is a continuous progression of SQL Injection attempts

> A)Done

Wanting to know more information about the attacker’s endpoint device, we take a peek at the ‘Endpoint Security’ tab and enter the IP Address of the attacker, where we get the following information:-

![](https://cdn-images-1.medium.com/max/1000/1\*afjfP0zS8BLXZOghSRC13A.png)

> Q)Analyze URL Address

> Analyze URL in 3rd party tools. Please click “Malicious” if it is malicious and click “Non-malicious” if it isn’t.

> You can use the free products/services below.

> AnyRun\
> &#x20;VirusTotal\
> &#x20;URLHouse\
> &#x20;URLScan\
> &#x20;HybridAnalysis

Let’s analyze using our go-to go tools VirusTotal and Hybrid-Analysis

Taking the URL — [http://nuangaybantiep.xyz](http://nuangaybantiep.xyz), and searching it up on [VirusTotal](https://www.virustotal.com/gui/home/upload) brought the following results:-

![](https://cdn-images-1.medium.com/max/1000/1\*D3wxzA9VSzbU5W6yIUTCDQ.png)

Says that the domain is not malicious at all\
Reading the comment under the ‘Community’ section brings the following note:-

![](https://cdn-images-1.medium.com/max/1000/1\*L2-yxFa8VtZvpFz9K5Z1kw.png)

That's why I stick by the rule of verifying with multiple platforms \
Reading Joe Sandbox’s [HTML report of the malicious domain](https://www.joesandbox.com/analysis/785029), we come across the following analysis of the domain:-

![](https://cdn-images-1.medium.com/max/1000/1\*94DRA5w\_3DKkkuvfKIUe1A.png)

Seems like a malicious domain and is capable of spreading Trojan(take a look at the pie chart)

Let’s analyze it on the [Hybrid-Analysis](https://www.hybrid-analysis.com) platform as well, where 2 search results pop up for the domain&#x20;

![](https://cdn-images-1.medium.com/max/1000/1\*u79cNM368Enx94Q0etOkrQ.png)

\
Both incidents determine that the file is not malicious through

![](https://cdn-images-1.medium.com/max/1000/1\*7HvuCLfgg9fzzzSrGmhYoQ.png)

Though the domain may be distributing malware, it’s not classified as a malicious domain by these threat intel platforms. So it’s safe to assume that it is suspicious and not malicious

Let’s click on “Non-malicious” and proceed forward

In the very next screen, we are asked to submit artifacts derived from the case

From the ‘Links’ tab of the domain’s analysis on VirusTotal, we can see some outgoing links from the suspicious domain

Unable to graph any mail addresses from this suspicious domain, we can very well state that the origin of the attack is from Reykjavik, the capital of Iceland&#x20;

![](https://cdn-images-1.medium.com/max/1000/1\*MherfU5aBFUIHfXLsIMUww.png)

This information was mapped from Maltego

## Our Artifacts&#x20;

![](https://cdn-images-1.medium.com/max/1000/1\*D2Ukxcw9nN6oZx7O9sm\_Ig.png)![](https://cdn-images-1.medium.com/max/1000/1\*9872SOCIgMNIQgHPXSCaFA.png)

## Analyst’s Note

![](https://cdn-images-1.medium.com/max/1000/1\*ZJjhy3CKKz-9U9QDSFUffA.png)

Finish the playbook!

Proceed to close the alert

![](https://cdn-images-1.medium.com/max/1000/1\*HDo8v2ywIraLlaZiXga1Gw.png)

## Alert Scorecard

Oops,5/10 is the score that we received. I will try to weed out mistakes in the future, to get a full score next time!&#x20;

![](https://cdn-images-1.medium.com/max/1000/1\*DQ1dScxg5CnbpmPyAGecjw.png)

## Conclusion

This SOC alert exercise was a breath of fresh air, as I performed threat hunting after repeated blue team activities on Try Hack Me.

Thank you for reading this blog entry. Stay tuned, as I go hunting some pcap files out there….

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by giving it a clap!
