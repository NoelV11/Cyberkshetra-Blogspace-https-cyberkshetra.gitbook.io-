# Let's Defend:  SOC147 - SSH Scan Activity Walkthrough

### Introduction

Welcome to the world of Blue Teaming, as I explore it on the Let's Defend Platform, a renowned site for Blue Team practice

Today, we are going to get our hands dirty, with the Easy SOC Analyst Alert - SOC147 - SSH Scan Activity

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FJeiGoPQBWH4Yf5q4Q1jg%2F2.png?alt=media\&token=076d2d5d-fa82-4e81-a8be-dbd62972db6d)

To start the SOC Investigation, we need to "undertake" the case. Woohoo! it is labeled as Malware!

We download the given .zip file onto a VM and unzip its contents,using the passphrase "infected"

### Enumeration

We get a file named 'nmap'. When running file command against it, we get information that it is a binary file

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FLXPSbajprIvhLz5Q8hwV%2F111.png?alt=media\&token=4035f4bd-88c6-4d45-8167-65f8b9d7b5ee)

Under the description, we find the hash for the file (3361bf0051cc657ba90b46be53fe5b36)

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FS9XYLICNTQhqdBP79gG8%2F110.png?alt=media\&token=61b785dd-7bf1-4197-92cc-94095d80b88a)

### Analysis

We run the hash on VirusTotal first, but it came with 0 flagged reports - no security vendors flagged the file as malicious

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FodRSbgYfbnxfpLHluTgQ%2F1.png?alt=media\&token=68a2bf07-5fd7-4f0e-a7c5-df5542241515)

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FMuMgE0bWaMOWGhrXdbPS%2F2.png?alt=media\&token=340b3d25-635e-4767-b861-6873b3649260)

Next,we run the file's hash on hybrid-analysis.com Under 'Report Search' - enter the hash

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2Fm3sUvsGRtytEZ5Z5GiGf%2F3.png?alt=media\&token=758fe954-f15d-43a9-bcec-230b2f975cbe)

There are many OS' acting like a sandbox- we get a hit for Linux 64bit. These are the malware's particulars:-

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FwKD1ILfWumdzPHuKyeKh%2F4.png?alt=media\&token=029710e4-316e-4cba-b475-3585aabb6de8)

We get some indicators as well:-

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2F4LLZMttAvIlS7hxSunuA%2F5.png?alt=media\&token=5364f6d4-d8aa-4a69-826a-4bc1cffc2b12)

Scrolling down,we get to visualize what the file looks like

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FNFHI1AdZxGz9Ihv31JrW%2F6.png?alt=media\&token=c7ce71cf-59be-4aea-afd8-5e25cb3e5afe)

We also get some extracted strings at the bottom (Important)

From the particulars given in the letsdefend.io site, about the .zip file, we find:-

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FghMpmgpWji1XagM0zaSG%2F7.png?alt=media\&token=65ce5ff7-9de0-4a7b-9a57-c30e95ca4213)

Now, let's take the IP Address - 172.16.20.5**.** We run it on the Endpoint Security and Log Management sections of LetsDefend

From the Log Management section, we get a lot of hits for the IP Address, but we try to narrow it down by the time, but don't get any matches for Jun 13,2021 - 04:23 PM (date and time stamp of SOC event occurrence)

Next, we move to Endpoint, where we paste the address and find a few particulars:-

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2F14l8ZoNYwSIvjJ4izWL4%2F8.png?alt=media\&token=3b5bcdde-d3ab-4cd9-bc8b-560f5c9c11d2)

Clicking on Command History,we get :-

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FyEqxmEUN8InrDHt1gVtC%2F9.png?alt=media\&token=2ea31857-9b7a-4306-9445-fda7e1e912ae)

Meaning - SSH Scan from 172.16.20.5 to targets in subnet 172.16.20.0/24

From Network Connections,we get:-

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FrEOLdPaczsr5yGdpzexV%2F9\(1\).png?alt=media\&token=af43f58b-69ad-4f9f-8c27-b19a31dc8667)

From Process List,we get:

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FSWVJ2Dtbui7fLY4S6zzr%2F10.png?alt=media\&token=2409ea8a-6bc7-4737-b591-e6c39ff1c49c)

There is nothing much to investigate further,so let's open the playbook and enter the data we have acquired till now

We enter our data and findings

### Results

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FqmlyKJ9prFaOHslWJZ7c%2F11.png?alt=media\&token=76d1f192-85be-4051-97b5-7e94a16eabaf)

_Let's Defend Questions:-_

_False Positive or not? - We clicked Yes (+5 points)_

_Malware or not? - No (-5 points) . The file was indeed malware._

_Check if malware is quarrantined or not - No (+5 points)_

Bonus - Just checked the 'Mailbox' feature in Let's Defend and searched the IP Address on the search bar,which threw up this email

![](https://noelatvitb.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FjXrTe5fpSNlEk4rpmYxs%2Fuploads%2FNiVKXWBY5TOtDDyaQAyg%2F12.png?alt=media\&token=c4d10c60-a416-4dbc-b0be-a30db69cbebe)

### Summary of Case

A malware file was analyzed,with threw a false positive to the SOC Team.The file infact contained the nmap scan report on hosts,within the 172.16.20.5/24 subnet.The malware file was'nt quarantined as well

Thank you for reading this entry.Stay tuned,as I go to hunt some pcap files out there....
