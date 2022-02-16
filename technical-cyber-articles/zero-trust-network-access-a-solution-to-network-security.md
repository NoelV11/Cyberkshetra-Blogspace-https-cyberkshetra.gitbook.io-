# Zero Trust Network Access-A solution to Network Security

Ever imagined being free from the constant fear of threats or malware, that could harm your device? Up to now, we never could have imagined being connected to a network, where everything relating to security, from top to bottom is decided by the authenticity of users. This idea introduces us to Zero Trust Network Access (ZTNA), one of the leading trends for Cyber Security, in 2021.

**NOTE:** Due to its sheer amount of occurrence, we will be depicting Zero Trust Network Access, by its acronym ZTNA from now on.

## Introduction

### What do you mean by ZTNA?

It refers to a network framework, of an organization, where users will have to provide proper identification for authentication, before being granted access to the network. This network contains access to in-house services and applications, that can be accessed only by authenticated users. Moreover, this network is private, without ever being connected to the Internet.\
In other words, it is a private network, that is hard to detect. It is compared to a castle-moat scenario, where residents of the castle are virtually protected by the moat and the castle is inaccessible to unauthorized laymen.

The concept was put forward, by John Kindervaag, a principal analyst, at Forrester Research Organization. This was built upon, by the occurrence of Operation Aurora, a cyber-attack, whose victim organization was Google, with Gmail accounts of Chinese dissidents being targeted. Moreover, it took a decade to implement.

&#x20;                                                  ![](https://cdn-images-1.medium.com/max/1000/1\*d-xDhPGI9v5ZICZUTTIgyQ.png)

&#x20;                                                      `Pictorial representation of ZTNA`

### **ZTNA-The need of the hour**

Before the dawn of ZTNA, attackers, having got past the network firewalls and security measures, were able to target devices (computers, workstations, mobiles) connected to the network, without any obstacles. Since devices were affected, it began the discussion of envisioning a framework, where devices would need to be authorized and authenticated as the baseline to gain entry to the network. The principle of “No Trust, until Verified,” can be applied here.

This concept gained more steam, when the pandemic struck, causing the workforce to work from home, due to the outbreak of the pandemic. A ZTNA is handled by a ZTNA Controller, who is assigned to monitor and verify the devices trying to log in to the network. Monitoring is done, by analyzing the geolocation of the device, timestamp, and date of login.

### **How?**

Since individuals were working remotely, due to the pandemic, their devices were connected to a VPN (organization owned). Since there is more threat to security and integrity, organizations have been gradually phasing out VPNs in favor of ZTNA.

**What are the measures of authentication?**

They include, but are not limited to:-

* Multi-factor authentication-It may include submission of confidential password, OTP/PassCode, or answering a predefined security question.
* Identity and Access Management-Usage of complex passwords(combination of symbols and alpha-numerics) and biometrics.
* Endpoint Security-Securing endpoints (devices), using authentication and encryption techniques, while connected on an enterprise’s network.

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*uqIIj2rRjkAjK-uF0tTlqA.png)

&#x20;                                            `ZTNA follows the Castle-moat security model`

## **Types of Zero Trust Network Architecture**

They include the following:-

* Endpoint Initiated ZTNA-Having previously defined devices as endpoints, these networks are monitored by the ZTNA Controller. Authorized users are given entry, after providing the correct credentials and are directed to an end-to-end encrypted network. In the unusual case of two devices, of the same user, trying to log in from different locations, it can be understood, that either one of the devices (or possibly both), has been compromised. In response, the user is flagged and is prevented from accessing the network.\
  &#x20;
* Service Initiated ZTNA-Unlike Endpoint ZTNA, which requires manpower to keep vigil, this architecture, instead, uses cloud technology, to accept/deny access to a network. This network contains a connector, that acts as a medium, between the cloud and network. Users are subjected to security measures, before gaining access. Most standard implementations of ZTNA follow this architecture.

BeyondCorp is an example of a service-initiated ZTNA, implemented by Google.

### **Features offered by ZTNA**

One interesting point to note is that software used by an enterprise can be accessed by simply being connected to the network, rather than connecting to the internet. This software is private and produced in-house. Users are protected from threats on the internet and being attacked by a black-hat hacker.

* Once a user is trying to gain access to the network (whether legitimately or else), the ZTNA will authenticate the user, with a directory of authorized users and roles working in the organization. At the same time, a push authentication notification is sent to the device, where the user can agree/deny access. It is a method for the network to verify that an authorized user is truly asking for access.
* Once logged on to the network, users are termed as “zero/least privileged”. This is done to ensure minimal attempts at initiating an attack. Attempting to access an application, will provide the user with a one-one interaction, with the app.
* Applications on the network, as specifically assigned to departments that they are useful in. For example, HR and Data Analyst teams will only be given access to MySQL Framework and cannot access other software applications.\
  &#x20;
* Micro segmentation-The term means to divide the vast network, to secure zones, to which assigned individuals can work. Individuals having access/gaining access to more than one zone will be flagged and recorded.

## D**isadvantages of ZTNA**

Despite being a fool-proof method to thwart intruders, it brings some issues to the surface, such as:-

* Over-privileged users-These users will have extensive access to the entire network (managers, supervisors) and can be the source of attacks. There is no restriction to perform actions, that may be unethical.
* Non-usage of protocols-ZTNA does not base itself on working, according to protocols, unlike firewalls or network hardware.
* End-of-life/legacy applications-Usage of software, such as Windows 7 and support for older versions of OS, on computer systems, can tend to be a vulnerable target. Ensure that all systems on the network are updated to the latest version of the OS, along with support drivers and security software.

## Conclusion

We can be sure, that ZTNA will make a foray into our existing network framework. Being a no-trust network, attackers can have a hard time trying to penetrate it. Moreover, the existence of this framework can spell the end of common network vulnerabilities.

Stay tuned and I will be back with a piece, specifically targeted for you mystery sleuths out there.

Thank you, for spending your precious time, digesting this article and I mean it.

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
