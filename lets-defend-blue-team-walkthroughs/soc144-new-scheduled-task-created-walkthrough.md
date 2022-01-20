# SOC144 - New scheduled task created Walkthrough

Hello readers, welcome to this blog entry. Today, we will be trying to solve the SOC144 - New scheduled task created alert, on the Let’s Defend platform.

\=====================================================================

### Introduction

The case particulars are given to analyze and understand:-​

![](https://cdn-images-1.medium.com/max/1000/1\*4-20uejooB2bNvYwp0k6Fg.png)

Next steps:-

> _Take ownership of case_

> _Create Case_

Download the file to be analyzed, onto the Virtual Machine (recommended) and unzip it

### Enumeration

We uncover a python file titled: ‘Sorted-Algorithm.py’

​

![](https://cdn-images-1.medium.com/max/1000/1\*pl8fDBFEumAEgsgnnVcf4w.png)

​Let’s have a look at its contents using the editor​

![](https://cdn-images-1.medium.com/max/1000/1\*BGeoABBCQtkMIwWdFPDKXA.png)

**​Gist of program:-**

> Sorts vowels twice (once in ascending and once in descending order) Takes second element of sorted element array and perform further perform sorting randomly and print the result

> Remeber that this script is designed to attack a host at IP — 92.27.116.104 and create a scheduled task named x86\_x64\_setup.exe,under the C:/Windows/Temp/ path

\=====================================================================

**Answering the Playbook’s Questions**

Now, let's open the alert’s playbook

Let’s start filling up details:-

​

![File Analysis](https://cdn-images-1.medium.com/max/1000/1\*N5B1Jp9O6k34p\_-2td8A-A.png)

### **File Analysis**

> Check if the malware is quarantined/cleaned

Let’s Defend recommends we check Log Management and Endpoint Security sections

Let’s go ahead with our Swiss Army Knife tools Hybrid-Analysis and VirusTotal

When tested on Falcon Sandbox, it found that the file was not malicious

​

![](https://cdn-images-1.medium.com/max/1000/1\*mFfnIpdrdi\_R-L3jGKt52A.png)

​

The same was the case with VirusTotal

​

![](https://cdn-images-1.medium.com/max/1000/1\*du\_27ttvBMT8yY4EdPP6ww.png)

​

We answer that the malware is cleaned

\=====================================================================

> Analyze Malware&#x20;
>
> Analyze malware in 3rd party tools and find C2 address

In this previous section, we had analyzed the artifact and deduced that the file was indeed not malicious

\=====================================================================

### **Adding artifacts to the casefile**

Let’s compile the information that we have collected:-

​![](https://cdn-images-1.medium.com/max/1000/1\*Ri-lHe9vyEDoSPPXpEkXqA.png)![](https://cdn-images-1.medium.com/max/1000/1\*VPOskGSP2kuLA8Djf15zIg.png)

### Analyst's Notes,about the alert

​

![](https://cdn-images-1.medium.com/max/1000/1\*7IhV\_1RgZSy9EKEwI0sm1g.png)

​Finish the Playbook

Close Alert — with notes, describing the alert as a True Positive

​

![](https://cdn-images-1.medium.com/max/1000/1\*ERfdQ19vwBWstSRcFUzzsA.png)

### **Alert Scorecard**

![](https://cdn-images-1.medium.com/max/1000/1\*DM0H8NdcsYhbje3qImlHjA.png)

​Points Acquired — 10/15.Not bad,not bad at all!

\=====================================================================

### **Summary of Case**

An incoming SOC Alert was briefed to us, about an RCE, that caused a process to be scheduled and executed. Upon analysis, the file in question did not throw up any malicious traces of activity, being described as danger-free by VirusTotal and Hybrid-Analysis tool.

\=====================================================================

### Conclusion

Thank you for devouring this blog entry and stay tuned as I try to close down more SOC alerts……
