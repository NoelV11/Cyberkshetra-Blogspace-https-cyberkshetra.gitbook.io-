# An in-depth analysis of an Intrusion Prevention System

Hello readers!

Who is in the mood to discuss some blue team and IPS today? Look what I've got for you,an article discussing about how an IPS works,threat detection methodology and it's implementation in an organization's network security architecture.

Grab some popcorn and read on!

## Introduction

In the implementation of a firewall (stateful or stateless), on a network, care is given to apply a detection system, that can detect and identify intruders, trying to break in. In comes the IPS, which is an automated network security device. It is an acronym for Intrusion Prevention System, which is handy in sensing DDOS attacks, brute force attacks, malware threats, and such.

The intrusion detection system that is applied sets 3 criteria for functionality:- Detection, Prevention, and Responsiveness

The functions of an IPS are to monitor transmissions, identify suspicious activities, compile logs of relevant transmission information, flag them and report them to the network administrator or concerned personnel.

It is, in many ways more effective than an IDS. When an IDS provides threat detection and nil prevention, IPS provides both detection and rectification of threats, on a network.

### **Why do these attacks take place?**

Attackers are constantly on the lookout for vulnerabilities, present on a network, whether it be weak authentication to gain access or misconfigured firewalls, with inadequate rules/protocols. The key is to not let exploitable spots lying around. The bigger the network, the more affected, users get.

## **How does detection take place?**

\
The device is constantly on the lookout for malicious activities or attempts to use network peripherals, without permission. Since this system is located behind a firewall, it can be applied as a filter, to provide an extra layer of security. By being on the lookout, the device thoroughly inspects each packet being transmitted through the network. A cross-check is done with the contents of the packet, with a database of known threats. Note that legitimate transmissions between nodes on the network are allowed to be carried out.

In case a packet gets flagged, the following actions are enforced:-\
Stop transmission from the source IP immediately.\
Dropping the packets being transmitted and \
Resetting the established connection.

The flagged source IP can be prevented from accessing the network ever again, or barred from using shared network peripherals and resources.

**What are the detection methods employed by an IPS?**

Detection methods maybe or can include:- \
Address Matching\
TCP connection analysis\
TCP Port matching

![](https://cdn-images-1.medium.com/max/1000/1\*eECJy0lxCq-SE5NHp4tIpg.jpeg)

&#x20;                      `A pictorial representation of an IPS`                           &#x20;

### **Methods that are undertaken to detect suspicious activity on networks**

* Signature-based detection-With each exploit exposed in the network, the signature (attack patterns) of the exploit is recorded to a dictionary. With each exploit, the IPS tries to match the signature of the exploit, with the ones recorded earlier. Note that these signatures are pre-defined and takes form in a sequence of bytes.
* Statistical Anomaly Detection-Here the network will have a calculated approximate on what constitutes a normal traffic pattern. This is established by a concept known as baseline performance level. The baseline always tries to match the current traffic. In case the traffic appears to be ‘not normal’, the transmission is aborted.\
  A reason for abnormal traffic is the illegitimate use of network bandwidth.
* Policy-based detection-In this method .rules/protocols are set on the Prevention System by the network admin. In case a packet, in a transmission, doesn’t follow the specified protocols, then the packet is dropped and transmission is aborted while raising an alert to the concerned personnel.

With the methods specified above, there are 3 Intrusion Prevention Systems that can be chosen, to meet requirements. They are:-

* Network behavior Analysis IPS (NIDS)-It’s primary function is to analyze the network for abnormal traffic flow, which is caused by threats. It is useful in preventing DDOS attacks and malware spread.
* Network-based Intrusion Prevention System (NIPS)-This system is instrumental in monitoring the network, for suspicious protocol activity.
* Host-based IPS (HIPS)-This architecture enables organizations, to monitor processes and user activity, over computer systems. It tracks changes that are made to system configuration and log files, ultimately alerting the personnel, about the suspicious activities

![](https://cdn-images-1.medium.com/max/1000/1\*pICSx4PqbFR4Nq2nHODSeA.jpeg)

&#x20;       `The importance of network security in today’s world is paramount`                &#x20;

## **Relative Advantages of an IPS**

* Constant vigilance, while supervising traffic flow
* Threat Detection and Prevention. It is not offered by an IDS.
* Network functions with the specified protocols, which are predefined
* Concerned Personnel are always in the loop, with a real-time alerting facility provided by IPS, in case a threat is detected.

## Conclusion

It is always wise to have a shield on your network, whether private or public. With the technology boom, we do have a basket of options to choose from, to enforce network security, be it a firewall or authentication system, from outside threats. Fortunately implementing an IPS solves that dilemma.

Well, thank you, for spending your precious time, digesting this article and I mean it.

Stay tuned and I will be back with an insight on Social Engineering affecting the security of computers and computer networks.

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
