# BTLO : Network Analysis-Web Shell challenge Walkthrough

Hello, blue teamers. In this blog entry, let’s take a crack at solving the [Network Analysis — Web shell](https://blueteamlabs.online/home/challenge/12), a retired challenge hosted on[ Blue Team Labs Online](https://blueteamlabs.online/home)

Let’s get our hands dirty with some .pcap files!

There’s also a [Gitbooks version](https://noelatvitb.gitbook.io/blue-team-investigations/lets-defend-blue-team-walkthroughs/soc-101-phishing-mail-detected-alert-walkthrough) of the same alert, written by me. You can go ahead and check it out

## The premise of the challenge

> The SOC received an alert in their SIEM for ‘Local to Local Port Scanning’ where an internal private IP began scanning another internal system. Can you investigate and determine if this activity is malicious or not? You have been provided a PCAP, investigate using any tools you wish.

Let’s proceed to open the .pcap file on Wireshark and answer the following questions:-

> Q)What is the IP responsible for conducting the port scan activity?

Sorting the packet stream by the TCP protocol, we can find that a host of machines (alive and responding) are being scanned by the host going under the address  — 10.251.96.4

![](https://cdn-images-1.medium.com/max/1000/1\*Vt47c7nN7tZFzPgxDCeMBQ.png)

> A) 10.251.96.4

> Q)What is the port range scanned by the suspicious host?

The easy way to get the range of ports that were scanned would be to take help from the ‘Conversations’ section, from the Statistics section

Sorting the entries by TCP, we can find that the scanned ports (port B) fall under the range of 1 -1024 (a common occurrence)

![](https://cdn-images-1.medium.com/max/1000/1\*TQClGCYoC2EnanyhRkjaxg.png)

> A)1–1024

> Q)What is the type of port scan conducted?

When filtering and analyzing the stream of TCP packets, we can see that a common pattern is followed — Attacker makes contact with victim (SYN) and receives an acknowledgment (ACK) from the scanned host, which follows the TCP SYN scanning method

![](https://cdn-images-1.medium.com/max/1000/1\*RggpNeFHLXyDOQfaFru5pw.png)

> A)TCP SYN

> Q)Two more tools were used to perform reconnaissance against open ports, what were they?

This question was a bit tricky, as I fell into a rabbit hole trying to enumerate TCP packets, for any traces of Nessus or Nmap tools being used

Later, when expanding my search to HTTP requests, I was able to crack it!

You need to apply the following packet filter:-

```
Filter — http.request.method == “GET”
```

![](https://cdn-images-1.medium.com/max/1000/1\*dgzWokgvbiviTFynaA6qTQ.png)

Analyzing the rest of the GET requests, we can see the same tool being used

Changing gears here, let’s target POST requests

Sure enough, we find the evidence of the next tool being used&#x20;

![](https://cdn-images-1.medium.com/max/1000/1\*hpTp7I\_x9gs0SZGw7P1SsQ.png)

> A)gobuster 3.0.1, sqlmap 1.4.7

> Q)What is the name of the php file through which the attacker uploaded a web shell?

Though I was able to identify that upload.php had been used to upload the shell, it was not being accepted as the answer

Expanding the packet entry, I found that the referer field was pointing to a different webpage, which could have probably been used for uploading the web shell

![](https://cdn-images-1.medium.com/max/1000/1\*07RkwkMCa80KXffwm1\_1Dg.png)

This is a new lesson I learned

> A)editprofile.php

> Q)What is the name of the wb shell that the attacker uploaded?

Filtering packets again by TCP, you can see the sequence where the attacker host accesses the Dbfunctions.php (the supposed web shell)

![](https://cdn-images-1.medium.com/max/1000/1\*ee0FBJHg0CqR\_pY-UGFK\_w.png)

> A)Dbfunctions.php

> Q)What is the parameter used in the web shell for executing commands?

Filtering packets again by HTTP, we can find that the parameter used is ‘cmd’

![](https://cdn-images-1.medium.com/max/1000/1\*C0vmrSbD6M7ynCCA1sb1-w.png)

> A)cmd

> Q)What is the first command executed by the attacker?&#x20;

This is evident from the above image

> A)id

> Q)What is the type of shell connection the attacker obtains through command execution?

This is the payload provided in the uploaded webshell&#x20;

![](https://cdn-images-1.medium.com/max/1000/1\*UJ2b0p-aMoFd6YCXM7GKBg.png)

From my previous pentesting gig, it was evident to me that this was an attempt to gain a reverse shell. Reverse shells are usually sent with the help of uploaded attachments and use attackers use netcat to receive the shell back

> A) reverse

> Q)What is the port he uses for the shell connection?

It is given in the reverse shell command&#x20;

> A)4422

## Conclusion

Thank you for reading this blog entry. Stay tuned, as I go hunting some pcap files out there….

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
