# ShellShock Attack: Let’s Defend Challenge

&#x20;                                        ![](https://cdn-images-1.medium.com/max/1000/1\*bbSSbnPCASB799173M8OSw.png)

Hello, blue teamers. Today I am going to try my hand on another short and easy blue team exercise from Let’s Defend, titled [Shellshock Attack](https://app.letsdefend.io/dfir/dfir/shellshock-attack/)

Let's go for it!

**NOTE: Always remember to investigate challenges from Let's Defend, on a VM.**

## Gist of the challenge

> You must to find details of shellshock attacks

> Log file: [https://app.letsdefend.io/download/downloadfile/shellshock.zip](https://app.letsdefend.io/download/downloadfile/shellshock.zip)\
> Pass: 321

> Note: pcap file found public resources.

## What is the Shellshock Vulnerability?

Quoting Wikipedia, **Shellshock**, also known as **Bashdoor**, is a family of [security bugs](https://en.wikipedia.org/wiki/Security\_bug) in the [Unix](https://en.wikipedia.org/wiki/Unix) [Bash](https://en.wikipedia.org/wiki/Bash\_\(Unix\_shell\)) [shell](https://en.wikipedia.org/wiki/Shell\_\(computing\)), disclosed on 24 September 2014. Shellshock could enable an attacker to cause Bash to [execute arbitrary commands](https://en.wikipedia.org/wiki/Arbitrary\_code\_execution) and gain unauthorized access to many Internet-facing services, such as web servers, that use Bash to process requests.

In fact, Vulnhub has a boot2root VM called Troll2, which is based upon the same vulnerability

## Challenge Questions

> Q) What is the server operating system?

Analyzing HTTP Packets give this answer (remember to expand them)

&#x20;                                     ![](https://cdn-images-1.medium.com/max/1000/1\*FnoGURi1wWS3YzlvbGG4ZQ.png)

> A) Ubuntu

> Q) What is the application server and version running on the target system?

Analyzing the HTTP packet with the Internal Server error gives us our answer

&#x20;                                         ![](https://cdn-images-1.medium.com/max/1000/1\*9J1k1I2qP2U7T-rIKf101Q.png)

> A) Apache/2.2.22

> Q) What is the exact command that the attacker wants to run on the target server?

&#x20;                                           ![](https://cdn-images-1.medium.com/max/1000/1\*X01cBGnswe\_VJd742jPeNw.png)

> A) /bin/ping -c1 10.246.50.2

## Conclusion

This challenge was a breeze!

Thank you for reading this entry. Stay tuned, as I try to close down some more SOC alerts....

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!.
