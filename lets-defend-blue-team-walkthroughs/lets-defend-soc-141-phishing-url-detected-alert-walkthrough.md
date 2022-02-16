# SOC 141 - Phishing URL Detected Alert

It’s the first week of February and that just means one thing. Let’s Defend has released a new set of SOC Alerts for us blue teamers to investigate and solve and here, we will be solving the SOC 141— Phishing URL alert.

Let’s jump right into it!

## Alert Details

![](https://cdn-images-1.medium.com/max/1000/1\*I3hagubgFizm9KduW\_rNIw.png)

Let’s take ownership of the case

Reading the alert’s summary, it’s plain to see that a phishing URL was sent to the victim, wanting him/her to click it&#x20;

Create a case book for the same

![](https://cdn-images-1.medium.com/max/1000/1\*IhrNdByQYnJR4nNXo3bggQ.png)

## Collection of Data

![](https://cdn-images-1.medium.com/max/1000/1\*IsHsvQjZA8GXI2h7Uy0i4g.png)

> Q)Please check alert details for the following below:-

> Source Address\
> &#x20;Destination Address\
> &#x20;User-Agent

From the alert summary, we can determine

> A)Source Address — 172.16.17.88\
> Destination Address — 192.64.119.190\
> User Agent — Mozilla — Windows

## Search Log

![](https://cdn-images-1.medium.com/max/1000/1\*HGoc3dU1RV1gyO96yxm2uA.png)

> Q)Please search in Log Management for details.

Let’s search the Source IP address, on the Log Management screen

We can see two corresponding entries for the address

![](https://cdn-images-1.medium.com/max/1000/1\*1XIgTGtl9Z4B7lzCqjF0dw.png)

Upon expanding the logs, we find the following information:-

![](https://cdn-images-1.medium.com/max/750/1\*4QHSAEiZaJKDKvWraa2JqA.png)![](https://cdn-images-1.medium.com/max/1000/1\*HxPRdZs3VX7lOxpHRA27xg.png)

## Analyze URL Address

> Analyze URL in 3rd party tools. Please click “Malicious” if it is malicious and click “Non-malicious” if it isn’t.

> You can use the free products/services below.

> AnyRun\
> &#x20;VirusTotal\
> &#x20;URLHouse\
> &#x20;URLScan\
> &#x20;HybridAnalysis

Let’s analyze using our go-to go tools VirusTotal and Hybrid-Analysis

Taking the URL —  [http://nuangaybantiep.xyz](http://nuangaybantiep.xyz), and searching it up on [VirusTotal](https://www.virustotal.com/gui/home/upload) brought the following results:-

![](https://cdn-images-1.medium.com/max/1000/1\*D3wxzA9VSzbU5W6yIUTCDQ.png)

It says that the domain is not malicious at all\
Reading the comment under the ‘Community’ section gives us the following note:-

![](https://cdn-images-1.medium.com/max/1000/1\*L2-yxFa8VtZvpFz9K5Z1kw.png)

That’s why I stick by the rule of verifying with multiple platforms \
Reading Joe Sandbox’s [HTML report of the malicious domain](https://www.joesandbox.com/analysis/785029), we come across the following analysis of the domain:-

![](https://cdn-images-1.medium.com/max/1000/1\*94DRA5w\_3DKkkuvfKIUe1A.png)

Seems like a malicious domain and is capable of spreading Trojan(take a look at the pie chart)

Let’s analyze it on the [Hybrid-Analysis](https://www.hybrid-analysis.com) platform as well, where 2 search results pop up for the domain

![](https://cdn-images-1.medium.com/max/1000/1\*u79cNM368Enx94Q0etOkrQ.png)

Both incidents determine that the file is not malicious through

![](https://cdn-images-1.medium.com/max/1000/1\*7HvuCLfgg9fzzzSrGmhYoQ.png)

Though the domain may be distributing malware, it’s not classified as a malicious domain by these threat intel platforms.

Let’s click on “Malicious” and proceed forward

## Has anyone accessed IP /URL Domain?

In the very next screen, we are asked to provide answers to the following questions:-

![](https://cdn-images-1.medium.com/max/1000/1\*uziesTQ07YN7r96NKZoKsA.png)

From the log expansion evidence provided above, we can answer these:-

> A)Apr, 04, 2021, 11:10 PM

> A)172.16.17.88

> A)192.64.119.190

> A)Mark

> A)Mozilla — Windows

> A)No

> A)Yes

### Containment

![](https://cdn-images-1.medium.com/max/1000/1\*HuvlujUgS7l6-zeRt\_C5CA.png)

Proceed to contain the victim host

## Submission of case artifacts

In the very next screen, we are asked to submit artifacts derived from the case

From the ‘Links’ tab of the domain’s analysis on VirusTotal, we can see some outgoing links from it

![](https://cdn-images-1.medium.com/max/1000/1\*ItuiouEHmNqculVc56aqxw.png)

Unable to graph any mail addresses from this suspicious domain, we can very well state that the origin of the attack is from Reykjavik, the capital of Iceland

&#x20;                                           ![](https://cdn-images-1.medium.com/max/1000/1\*MherfU5aBFUIHfXLsIMUww.png)

&#x20;                          `Mapped using Maltego`                                         &#x20;

![](https://cdn-images-1.medium.com/max/1000/1\*xZIv5OG0mX3l9asIgRo5Sg.png)

This is what the malicious domain looks like

## Case Artifacts

![](https://cdn-images-1.medium.com/max/1000/1\*fQ\_K5wZ9w5IoLJr7n6urBw.png)

## Analyst’s Note

![](https://cdn-images-1.medium.com/max/1000/1\*lXaKfnPcEQJtGsX-cpQMpw.png)

Finish the playbook!

![](https://cdn-images-1.medium.com/max/1000/1\*OXqkm5CCe7T\_02IPpRVEog.png)

### Close Alert

Proceed to close the alert and provide parting remarks about the case

![](https://cdn-images-1.medium.com/max/1000/1\*UrXY4s9b0PgIBD0VW2HYDQ.png)

## Alert Scorecard

This is awesome!

![](https://cdn-images-1.medium.com/max/1000/1\*UwZqN6T6f9jdrq\_FCU\_XEQ.png)

## Conclusion

This SOC alert exercise was a breath of fresh air, as I performed threat hunting after repeated blue team activities on Try Hack Me.

Thank you for reading this blog entry. Stay tuned, as I go hunting some pcap files out there….

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
