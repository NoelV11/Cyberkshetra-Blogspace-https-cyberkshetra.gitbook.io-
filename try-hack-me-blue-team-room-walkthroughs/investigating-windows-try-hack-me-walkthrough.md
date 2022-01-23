# Investigating Windows:Try Hack Me Walkthrough

![](../.gitbook/assets/IW.png)

Hello fellow blue teamers! Join me in this blog entry,as I attempt to solve the [Investigating Windows](https://tryhackme.com/room/investigatingwindows) room,on Try Hack Me.This room is of Medium Difficulty

Room creation credits go to[ tryhackme](https://tryhackme.com/p/tryhackme).Thank you!

## Investigating Windows

This is a challenge that is exactly what is says on the tin, there are a few challenges around investigating a windows machine that has been previously compromised.Connect to the machine using RDP. There is no need of connecting to the VPN or making use of Attackbox

The credentials for the machine are as follows:

Username: Administrator&#x20;

Password: letmein123!

Start the attached Virtual Machine.The attackbox is not required for this task.

### **Questions**

> **Q)**Whats the version and year of the windows machine?

This question can be solved mainly in two methods:-

1\)Via GUI

Navigate to Windows Start -> Settings -> System -> About

Where we find the following info:-

​​![](https://cdn-images-1.medium.com/max/1000/0\*3eLMh5IRcVsMZphd)​

Alternatively we can use CMD

`Command — systeminfo`​​

![](https://cdn-images-1.medium.com/max/1000/0\*XhxCW8dMQBhhmit6)​

> A)Windows Server 2016

> Q)Which user logged in last?

We make use of Event Viewer for this task,navigating to Windows Logs->Security

When sifting through recent logs,we can find this entry:-​

​![](https://cdn-images-1.medium.com/max/1000/0\*VLsOQo4GgxnLqonU)​

> A)Administrator

> Q)When did John log onto the system last?

> Answer format: MM/DD/YYYY H:MM:SS AM/PM

How to find users on a system?We make use of CMD,to find the enumerate this answer

`Command - net user john`

Where we find:-

​​![](https://cdn-images-1.medium.com/max/1000/1\*jlCem3\_gUShjeRXI\_UgYOA.png)​

> A)03/02/2019 5:48:32 PM

> Q)What IP does the system connect to when it first starts?

When booting up the system,we see this CMD Screen connecting to System Internals:-​​![](https://cdn-images-1.medium.com/max/1000/1\*4Sghm33gwBx79Z6AAncqHw.png)​

> A)10.34.2.3

> Q) What two accounts had administrative privileges (other than the Administrator user)

> Answer format: username1, username2

​​![](https://cdn-images-1.medium.com/max/1000/1\*clROgXCs3UQYa40UN-qJJA.png)​

> A)Jenny,Guest

> Q)At what time did Windows first assign special privileges to a new logon?

> Answer format: MM/DD/YYYY HH:MM:SS AM/PM

> A)03/02/2019 04:04:49 PM — from analysis of Windows Event

> Q)Whats the name of the scheduled task that is malicous.

A)New Knowledge:We have a ‘Task Scheduler’ app on Windows

Clicking on it,we find:-​

​![](https://cdn-images-1.medium.com/max/1000/1\*taRc3h4hfl5uHf38TB\_ODw.png)​

Out of these,Clean file system looks like the real deal

> A)Clean file system

> Q)What file was the task trying to run daily?

From the scheduled task’s description,we find:-​

​![](https://cdn-images-1.medium.com/max/1000/1\*Yj2nLJb6AFISN4j\_NCG5LQ.png)​

> A)nc.ps1

> Q)What port did this file listen locally for?

> A)1348

> Q)When did Jenny last logon?

> A)Never

​​![](https://cdn-images-1.medium.com/max/1000/1\*JPjmIMPB\_M1egzPgDcSMOg.png)​

> Q)At what date did the compromise take place?

Answer format: MM/DD/YYYYWhen moving to Scheduled Event ->Triggers,we find the start date of this process

> A)03/02/2019

> Q)What tool was used to get Windows passwords?

I noticed there is a task called “GameOver” under the action tab,under the Clean file system scheduled task .I saw there is a executable called “mim.exe” located at TMP directory of the system it triggered every 5 min.

Explains why Mimikatz opens up once in a while​

​![](https://cdn-images-1.medium.com/max/1000/1\*h95mehKJAi5C\_fv8UGp5vw.png)​

Upon inspecting it,we find (under ‘Actions’ tab)

​​![](https://cdn-images-1.medium.com/max/1000/1\*9Y--YcMmR6Y7PoQkGHGFRw.png)​

> A)mimikatz

> Q)What was the attackers external control and command servers IP?

We have two methods to find this out:-Consult C:\Windows\System32\drivers\etc\hosts,from CMD

`Command — type C:\Windows\System32\drivers\etc\hosts`.Where we find:-​​![](https://cdn-images-1.medium.com/max/1000/1\*cz2xuwcCg4th2pl2ejEbyQ.png)​

From here,we can see that Google’s IP Address/DNS Address is given as 76.32.97.132,when it should be 8.8.8.8

> A)76.32.97.132

> Q)What was the extension name of the shell uploaded via the servers website?

A)We can browse C:\inetpub\wwwroot .to find any files uploaded in web browser

Where,we find:-

​​![](https://cdn-images-1.medium.com/max/1000/1\*UI5woFTKEFhlJxJqhtC0xg.png)​

> A).jsp

> Q)What was the last port the attacker opened?

We can check the last open port by examining the inbound rules on the Windows Firewall and analyze the first entry,titled “Allow outside connections for development”​​

![](https://cdn-images-1.medium.com/max/1000/1\*g2TI1hvTDfLO2QHgDvCz9A.png)​

We find port 1337 as the last port to be opened,by the attacker,for inbound traffic

> A)1337

> Q)Check for DNS poisoning, what site was targeted?

A)We observed in the above picture that Google had it’s default IP )8.8.8.8.)changed to some other IP in,in a manner this mimicks the “DNS Posioning Attack”

> A)google.com

## Conclusion

This room allowed me to be a bit more comfortable with Active Directory,which is a good skill to have,while following the SOC Analyst learning pathway.

I am much more confident about my skills and look forward to learning more on Try Hack Me.Thank you for reading this blog and stay tuned as I try to close down more SOC alerts……
