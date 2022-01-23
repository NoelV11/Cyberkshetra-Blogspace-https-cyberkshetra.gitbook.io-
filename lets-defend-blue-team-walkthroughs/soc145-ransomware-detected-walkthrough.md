# SOC145 - Ransomware Detected Walkthrough

Welcome to this blog entry,as I document my journey,into the world of blue teaming.We will be tackling the “SOC145 — Ransomware Detected” case on the Let’s Defend platform,which is of hard difficulty

Let’s jump head first into it.

### Introduction to Case

Case Particulars provided to the analyst:-

![](https://cdn-images-1.medium.com/max/1000/0\*pFsfqeuj6ztYVXG1)

We first take a look at the mailbox,to find any pointers about the case —which we couldnt find

### Enumeration

Now take the IP Address — 172.16.17.88 and perform a check on the endpoint and log sections

We get this from the Endpoint section,giving a description about the source IP Address’ host machine​

![​](https://cdn-images-1.medium.com/max/1000/0\*VqWijjynjbcW2TSS)

> Endpoint Machine Name — MarkPRD

> Windows 10 OS

> User name — MarkGuna&#x20;

> Last Login — Aug 29 2020 08:12 PM

No entries were found for Browser,Network or Command History.We get these entries for Process List however:-

​![](https://cdn-images-1.medium.com/max/1000/0\*myZhuPhg5evsUWM4)![](https://cdn-images-1.medium.com/max/1000/0\*43o1hhwj1bOnjity)

We get a corresponding match for someone named Mark,recieving a mail on Aug 29,when conducting a more through search in the LetsDefend mailbox​

![](https://cdn-images-1.medium.com/max/1000/0\*ZCWvvFp27Hi8RuAr)

### Analysis of Evidence

Having performed initial enumeration,lets download the file and unzip it,using the passphrase:infected

We uncover a file named ab.bin.Running file command against it tells us that it is an executable file,with GUI Interface

​![](https://cdn-images-1.medium.com/max/1000/0\*78m7i2fZ3Jr2vkHs)

Next,we take the file for analysis on VirusTotal and Hybrid-Analysis tools

\====================================================================

### **Reconnaisance using Hybrid-Analysis**

Hybrid Analysis — (File is classified as Ransomware)

Related Hash — d5e2584ff2c17966ac150adfaeaab508af50354c7611884d64207d9c5d6b969c​

![](https://cdn-images-1.medium.com/max/1000/0\*-I5\_\_yHAWSDhdTRC)

File Analysis of the file on Hybrid-Analysis brings us:-

![](https://cdn-images-1.medium.com/max/1000/0\*Q2GkYsmfdTePd9hu)

### **Reconnaisance on Virus Total**

VirusTotal — 60/68 vendors find the file suspicious

Threat Name — Avaddon (dark web intelligence)

MD5 Hash of malicious file — 0b486fe0503524cfe4726a4022fa6a68

Executed Shell commands and process tree of the suspected file

![](https://cdn-images-1.medium.com/max/1000/0\*iSUI62NQ3Lwh\_hkn)

More notes about the ransomware file

​

![](https://cdn-images-1.medium.com/max/1000/0\*39xHpcgKpPT3GpjV)

No relevant HTTP Traffic or DNS Requests for this file(checked on Hybrid Analysis).This is a big blow,as we don't know the origin (country) of the ransomware

IOC’s of infected file —Suspicious and Malicious

​![](https://cdn-images-1.medium.com/max/1000/1\*xtgfPJJFoFG9DWXF5yUf8A.png)![](https://cdn-images-1.medium.com/max/750/1\*QJ7V5yM\_gK\_r0IqhkQu1Qg.png)

### **Steps to solve and close this Ransomware alert**

> Create a case

> We select ‘Other threat indicator’ as classification for this file Malware quarratined or not? — No File is malicious or not? — Yes Check if any address accessed this malicious file? — Yes (we found IP- 81.169.145.105 had accessed this file,from the Log section)

> Contain the machine — Yes&#x20;

> Now,we add artifacts to the case:-

> IP Address 81.169.145.105 — Address that accessed the malicious file&#x20;

> IP Address 172.16.17.88 — Source address of ransomware&#x20;

> MD5 Hash 0b486fe0503524cfe4726a4022fa6a68 — Hash of file

> Finish Playbook

> Close the alert and state that it is a true positive

### **Alert Scorecard**

![](https://cdn-images-1.medium.com/max/1000/1\*5nmj43q3OAIiJnxqj28qAQ.png)

15/20 points acquired! That’s not bad in my book!

\====================================================================

### **Summary of Case**

A SOC alert came in,detailing the case as Ransomware.Analysing the file brought us to the conclusion that it was a binary file.Further enumeration found that the file was flagged previously on security and sandbox platforms,where we were able to gather more intelligence about the suspected file,concluding the alert to be a true positive

\====================================================================

### Conclusion

Thank you for devouring this blog entry and stay tuned as I try to close down more SOC alerts……
