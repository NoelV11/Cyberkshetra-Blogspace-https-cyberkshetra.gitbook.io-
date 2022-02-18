# BTLO: Suspicious USB Stick Challenge

&#x20;                                     ![](https://cdn-images-1.medium.com/max/1000/1\*Cb6k216iRs34XnDD504KNg.png)

Hello, blue teamers. In this blog entry, join me as I attempt to conquer the [Suspicious USB Stick challenge](https://blueteamlabs.online/home/challenge/5), hosted on [Security Blue Team Labs Online](https://blueteamlabs.online/home). This is a retired challenge and falls under the Digital Forensics domain. It was pretty fun to investigate!

**NOTE: Always remember to investigate challenges from BTLO, on a VM.**

## Premise of Alert

> One of our clients informed us they recently suffered an employee data breach. As a startup company, they had a constrained budget allocated for security and employee training. I visited them and spoke with the relevant stakeholders. I also collected some suspicious emails and a USB drive an employee found on their premises. While I am analyzing the suspicious emails, can you check the contents on the USB drive?

Let’s start

Download the USB Image attached with this task. In my opinion, it is better to unzip and extract the files, using GUI mode

Opening the attachment, we get these files:-

&#x20;                                        ![](https://cdn-images-1.medium.com/max/1000/1\*cHp54X2QybuAdYZoj2\_nxQ.png)

Proceed to unzip the USB.zip file using the passphrase ‘btlo’ and get the USB directory.

Extract it in your Downloads file. Inside this directory, we get:-

&#x20;                                          ![](https://cdn-images-1.medium.com/max/1000/1\*o2EezUCsLkEq5\_VqSnBQsg.png)

## Enumeration of evidence

Opening the README.pdf file to view its contents, we see the following text:-

&#x20;                                            ![](https://cdn-images-1.medium.com/max/1000/1\*RK57x1e3CnxXX7u-hdo5Vg.png)

Opening up the autorun.inf file, we can see the following instructions:-

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*yqu5yguwbU3CuAxAkturyw.png)

Let’s answer the challenge questions:-

> Q) What file is the autorun.inf running?

> A) README.pdf

## Analysis of malware sample

> Q) Does the pdf file pass Virustotal scan? (No malicious results returned)

Let’s submit this file for analysis on [VirusTotal](https://www.virustotal.com/gui/home/upload).The following report is received, indicating that the file is indeed malicious

&#x20;                                       ![](https://cdn-images-1.medium.com/max/1000/1\*wSpAEc4f-ORqUT21Kwj9cA.png)

> A) False

## Magic Numbers anyone?

> Q) Does the file have the correct magic number?

To test this, I suggest reading this [article](https://www.geeksforgeeks.org/working-with-magic-numbers-in-linux/#:\~:text=Some%20files%2C%20however%2C%20do%20not,the%20case%20of%20text%20files%29.\&text=Magic%20numbers%2FFile%20signatures%20are,xxd%27%20command%20as%20mentioned%20below.). Magic numbers are usually used to indicate and differentiate the formats of files. These numbers are visible on hex editors

From a quick google search, we find that the magic number of a PDF file is- (hex 25 50 44 46 )

Going to our CLI and testing out the following command

```
Command — xxd README.pdf | head
```

&#x20;                                          ![](https://cdn-images-1.medium.com/max/1000/1\*UR2ScJrWvMb55uKm0veIMg.png)

From the first line of the output, it is evident that the PDF file is not disguised in any way

> A) True

> Q) What OS type can the file exploit? (Linux, MacOS, Windows, etc)

To understand the payload executed by any malicious file, it’s wise to see the actions taken by it. It is viewable from the ‘Behaviour’ section for this file, on VirusTotal

&#x20;                                       ![](https://cdn-images-1.medium.com/max/1000/1\*Hyw7eexHew3OQPh6\_lr4kA.png)

It is evident that the payload targets Windows systems and spawns Windows processes

> A) Windows

> Q) A Windows executable is mentioned in the pdf file, what is it?

To extract strings from this malicious PDF, I prefer uploading it to [Hybrid-Analysis](https://www.hybrid-analysis.com) and then filtering it out by .exe.Two hits are received

&#x20;                                          ![](https://cdn-images-1.medium.com/max/1000/1\*IsOSt\_cvL51LvptI69txUQ.png)

> A) cmd.exe

## Hunting down suspicious elements

> Q) How many suspicious /OpenAction elements does the file have?

Executable files are always flagged by antivirus tools and are increasingly treated as suspicious and untrusted by default. PDF files are instead treated with less suspicion and attackers often use them to trick targets into running malicious code, to obtain an initial foothold into their machines.

Code obfuscation and other techniques are used in malicious PDF files to bypass antiviruses. Therefore, in case of suspicion, it is useful to check the file manually.

Luckily for us, PDFs can identify suspicious elements, which we can identify by using [pdf-parser.py](https://blog.didierstevens.com/programs/pdf-tools/).This is a CLI tool, that can pull out the information we want. Download it

```
Syntax — python3 pdf-parser.py <file.pdf>
```

Running the script against the PDF file and skimming along with the results, we find that 1 suspicious action was found

> A) 1

Challenge conquered!

&#x20;                                       ![](https://cdn-images-1.medium.com/max/1000/1\*7wigTigZwWkDbMXjb6z6pA.png)

## Conclusion

It is good to experiment and practice analysis with malware, especially when you finally get exposed to one in a SOC environment. These small tasks are sure to help me in the future

Thank you for reading this blog entry. Stay tuned, as I go hunting behind some pcap files out there.....

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
