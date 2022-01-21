# Try Hack Me's Splunk:A Walkthrough

Splunk — Try Hack Me

Task 1 — Deploy

Deploy the Splunk virtual machine. This can take up to five to ten minutes to launch. If the webpage does not load for you after ten minutes, terminate and relaunch the machine.

Username: splunkadmin

Password: AdminAdmin01

Task 2 — Can you dig it?

A short quiz over the base search commands that are useful for Splunk. All you’ll need for this is the attached quick reference guide and possibly the magic of Google. Include all parts of the search query unless otherwise instructed.

Download the quick reference file

Enjoy the room! For future rooms and write-ups, follow [@darkstar7471](http://twitter.com/darkstar7471) on Twitter.

\========================================

Answer the questions below

> Q)Splunk queries always begin with this command implicitly unless otherwise specified. What command is this? When performing additional queries to refine received data this command must be added at the start. This is a prime example of a slight trick question.

> A)search

\


> Q)When searching for values, it’s fairly typical within security to look for uncommon events. What command can we include within our search to find these?

> A)rare

\


> Q)What about the inverse? What if we want the most common security event?

> A)top

\


> Q)When we import data into splunk, what is it stored under?

> A)index

Knowledge Nugget:All data in Splunk is stored in an index and in hot, warm, and cold buckets depending on the size and age of the data

> Q)We can create ‘views’ that allow us to consistently pull up the same search over and over again; what are these called?

> A)dashbard

\


> Q)Importing data doesn’t always go as planned and we can sometimes end up with multiple copies of the same data, what command do we include in our search to remove these copies?

> A)dedup

\


> Q)Splunk can be used for more than just a SIEM and it’s commonly used in marketing to track things such as how long a shopping trip on a website lasts from start to finish. What command can we include in our search to track how long these event pairs take?

> A)transaction

\


> Q)In a manner similar to Linux, we can ‘pipe’ search results into further commands, what character do we use for this?

> A)|

\


> Q)In performing data analytics with Splunk (ironically what the tool is at it’s core) it’s useful to track occurrences of events over time, what command do we include to plot this?

> A)timechart

\


> Q)What about if we want to gather general statistical information about a search?

> A)stats

\


> Q)Data imported into Splunk is categorized into columns called what?

> A)fields

\


> Q)When we import data into Splunk we can view it’s point of origination, what is this called? I’m looking for the machine aspect of this here.

> A)host

\


> Q)When we import data into Splunk we can view its point of origination from within a system, what is this called?

> A)source

\


> Q)We can classify these points of origination and group them all together, viewing them as their specific type. What is this called? Use the syntax found within the search query rather than the proper name for this.

> A)sourcetype

\


> Q)When performing functions on data we are searching through we use a specific command prior to the evaluation itself, what is this command?

> A)eval

\


> Q)Love it or hate it regular expression is a massive component to Splunk, what command do we use to specific regex within a search?

> A)rex

\


> Q)It’s fairly common to create subsets and specific views for less technical Splunk users, what are these called?

> A)pivot table

\


> Q)What is the proper name of the time date field in Splunk

> A)\_time

\


> Q)How do I specifically include only the first few values found within my search?

> A)head

\


> Q)We can collect events into specific time frames to be used in further processing. What command do we include within a search to do just that?

> A)bucket

\


> Q)We can also define data into specific sections of time to be used within chart commands, what command do we use to set these lengths of time? This is different from the previous question as we are no longer collecting for further processing.

> A)span

\


> Q)When producing statistics regarding a search it’s common to number the occurrences of an event, what command do we include to do this?

> A)count

\


> Q)Last but not least, what is the website where you can find the Splunk apps at?

> A)splunkbase.splunk.com

\


> Q)We can also add new features into Splunk, what are these called?

> A)apps

\


> Q)What does SOC stand for?

> A)Security Operations Center

\


> Q)What does SIEM stand for?

> A)Security Information and Events Management

\


> Q)How about BOTS?

> A)Boss of the SOC

\


> Q)And CIM?

> A)Common Information Model

\


> Q)what is the website where you can find the Splunk forums at?

> A)community.splunk.com

Task 3 — BOTS!

Check out BOTS! — [https://cyberdefenders.org/search/labs/?q=Boss](https://cyberdefenders.org/search/labs/?q=Boss)

Task 4 — Halp,I’m drowining in logs!

Navigate to the webpage found at 10.10.61.42:8000 on the machine you’ve deployed for this room. The credentials for logging into Splunk are as follows:

Username: splunkUser

Password: SplunkUser#321

Upon being redirected to this webpage,we can see that the site has been heavily defaced

![](https://cdn-images-1.medium.com/max/1000/1\*gqcsDErY79a8pqvZ1HvQdQ.png)

Given data by Sourcetypes

![](https://cdn-images-1.medium.com/max/1000/1\*EUNx5D4jMglxcSAjZXxtyA.png)

These two images are the two scenarios we will be working through throughout this room. In addition to this, we will be using Lockheed Martin’s Kill Chain to break down each attack and report it accordingly.

\


![](https://cdn-images-1.medium.com/max/1000/0\*vUvlT90xeufwIG\_I)

\
Task 5 — Advanced Persistant Threat

Work your way through the first scenario in order to track down P01s0n1vy! Don’t hesitate to use the material provided to give you a nudge!

The most important information provided by any log entry is the metadata associated with it.We can find itsy-bitsy details of interest like timestamps of incident,type of web requests and so on.

So,let’s get our feet wet and learn how to sort logs by metadata

> Query — | metadata type=sourcetypes index=botsv1

\=====================================================================\
Scenario — 1

APT

\


![](https://cdn-images-1.medium.com/max/1000/1\*gqcsDErY79a8pqvZ1HvQdQ.png)

In this scenario, reports of the below graphic come in from your user community when they visit the Wayne Enterprises website, and some of the reports reference “P01s0n1vy.” In case you are unaware, P01s0n1vy is an APT group that has targeted Wayne Enterprises. Your goal, as Alice, is to investigate the defacement, with an eye towards reconstructing the attack via the Lockheed Martin Kill Chain.

During the scenario, we will build both Kill Chain and traffic flow diagrams to help visualize what has happened. While investigating, you may find yourself working backward to reconstruct an attack, but you may also find yourself in the middle of the Kill Chain based on indicators that are identified. If this happens, you must work BOTH backward to reconstruct the past but also forward to find if additional actions have transpired. For simplicity in this exercise, we will build across the Kill Chain using Splunk, starting with reconnaissance the adversary took and build things out as they move through the Kill Chain.&#x20;

> Q)What is the likely IP address of someone from the P01s0n1vy group scanning imreallynotbatman.com for web application vulnerabilities?

We can run the following Splunk query

> Query — index=botsv1 iamreallynotbatman.com\
> Knowledge Nugget:index — new data imported to Splunk are stored in indexes

We get a total of 78683 hits\
From the first query itself,we can find the following information:-

![](https://cdn-images-1.medium.com/max/1000/1\*xvvditOndjQtM-HN3cLRbA.png)

> **REMEMBER**:Here,source IP — Our Web Server’s IP\
> Destination IP — Attacker’s IP

\
Splunk classiied sourcetypes for this query — Suticata \
So the attacker’s IP scanning our server is 40.80.148.42

> A)40.80.148.42

\


> Q)What web scanner scanned the server?

Since we know from answering the prior question that web vulnerability scans originated from the particular source IP 40.80.148.42, we can search for traffic from 40.80.148.42 and examine the src\_headers for clues related to the tool being used for the scan.

> Query — index=botsv1 src = 40.80.148.42 sourcetype=stream:http

We get a total of 21029 events here

Now,let’s try to analyze the HTTP Headers for any clues

From the log entry dated — 8/10/16,at 10:22:27.612 PM,we can find the following entry made in src\_headers

![](https://cdn-images-1.medium.com/max/1000/1\*ihZPaLlZ-4Nu6-eciXJdYA.png)

> A)Acunetix

\


> Q)What is the IP address of our web server?

\


> A)192.168.250.70 (it’s evident from the logs above)&#x20;

\


> Q)What content management system is imreallynotbatman.com using?

We can find this answer, by running the same query\
\


> Command — index=botsv1 iamreallynotbaroman.com

We can find this information easily,in one of the recent logs

![](https://cdn-images-1.medium.com/max/1000/1\*QzeqykgcP\_0pdzjSHN7xbw.png)

> A)Joomla

\


> Q)What address is performing the brute-forcing attack against our website?

As this is a web-based attack,we can search and filter HTTP packets and further refine it w,ith trafic being directed to 192.168.270.50 (target host)

> Query — index botsv1 sourcetypr=stream:http dest = “192.168.270.50”

8213 results arise

Now to cheeck which IP is bruteforcing attacks aginst us

Inspecting ‘fields’ filter

![](https://cdn-images-1.medium.com/max/1000/1\*izgSp\_Y2Mc9TBvErnb5Zpw.png)

Selecting the c\_ip field,gives us 3 values in total:-

![](https://cdn-images-1.medium.com/max/1000/1\*ov-o-8ah9kXOUk5VhFswTA.png)

The only outlier we see here is IP — 23.22.63.114,as we know the other hosts are source and destination respectively

> A)23.22.63.114

\


> Q)What was the first password attempted in the attack?

Since the attack is web based,the passwords are likely to have been inserted on some login page,hence generating “POST” requests,from the web browser

Adding this additional parameter to our query

> Query— index=botsv1 sourcetype=stream:http dest=”192.168.250.70" http\_method=POST

Since the question requires us to input the very first password used in the bruteforce attack,we sift through 21 pages of log entries to find the first incident,that occured on 8/10/16 9:45:21 PM

\


![](https://cdn-images-1.medium.com/max/1000/1\*d0lzShJtUP63L7\_FohFn9g.png)

Which can also be found,when running the following Splunk query

> Query— index=botsv1 sourcetype=stream:http dest=”192.168.250.70" form\_data=\*username\*passwd\* | reverse

Let’s further add date and time stamps here for easy understanding

> Query — index=botsv1 sourcetype=stream:http dest=”192.168.250.70" form\_data=\*username\*passwd\* table\_time | reverse

\


> A)123456789

\


> Q)One of the passwords in the brute force attack is James Brodsky’s favorite Coldplay song. Which six character song is it?

Since I am a regular Coldplay listener,their songs are familaiar to me like the back of my hand,so on Page 17 of Log entries,I found a sweet surprise!

![](https://cdn-images-1.medium.com/max/1000/1\*IWiDC0j0VmVu5eyvix05HQ.png)

> A)Yellow

Fun Trivia:Yellow’s music video **shot entirely in slow motion** and features frontman Chris Martin walking alone along the beach.

> Q)What was the correct password for admin access to the content management system running imreallynotbatman.com?

Naturally a password bruteforce attack stops when the correct password is eventially found and that is the latest log entry,present on Page 1

![](https://cdn-images-1.medium.com/max/1000/1\*OyvefJaj89yASqEgGavWMA.png)

No surprises there heh!

> A)batman

\


> Q)What was the average password length used in the password brute forcing attempt rounded to closest whole integer?

To do this,we have three queries to run:-

> Query — Extracting passwords from requests — index=botsv1 sourcetype=stream:http form\_data=\*username\*passwd\* \
> \| rex field=form\_data “passwd=(?\<userpassword>\w+)” \
> \| head 10 \
> \| table userpassword

(for now,let’s extract the first 10 passwords)

Next,we calculate the lengths of the extracted passwords

> Query — index=botsv1 sourcetype=stream:http form\_data=\*username\*passwd\* \
> \| rex field=form\_data “passwd=(?\<userpassword>\w+)” \
> \| eval lenpword=len(userpassword) \
> \| head 10 \
> \| table userpassword lenpword

![](https://cdn-images-1.medium.com/max/1000/1\*Fh63SEtIWLfJiXjwLOja8Q.png)

Now,let’s refine our results

> Query — index=botsv1 sourcetype=stream:http form\_data=\*username\*passwd\* \
> \| rex field=form\_data “passwd=(?\<userpassword>\w+)” \
> \| eval lenpword=len(userpassword) \
> \| search lenpword=6 \
> \| table userpassword lenpword

We pull out all passwords,of length 6

![](https://cdn-images-1.medium.com/max/1000/1\*RZZcVvTkNjIDabVIUdWdFA.png)

> A)6

\


> Q)What was the average password length used in the password brute forcing attempt rounded to closest whole integer?

A)From the log analysis,we hace determined that the password ‘batman’ was used twice — once used to bruteforce the password and the other occurence was to login with the password,each from different passwords

Now,let’s construct a query to find the objective of this question,i.e to find average password length&#x20;

> Query — index=botsv1 sourcetype=stream:http\
> \| rex field=form\_data “passwd=(?\<userpassword>\w+)” \
> \| search userpassword=batman \
> \| transaction userpassword \
> \| table duration

![](https://cdn-images-1.medium.com/max/1000/1\*OukxDCy6lk3Yi-VN0B19TA.png)

> A)92.17

\


> Q)How many unique passwords were attempted in the brute force attempt?

\


> Query — index=botsv1 sourcetype=stream:http form\_data=\*username\*passwd\* | rex field=”form\_data \*passwd=(?\<usernamepasswd>\w+)” | stats dc(usernamepasswd)

where,dc — distinct count

> A)412

\


> Q)What is the name of the executable uploaded by P01s0n1vy?

\


> Query -index=botsv1 sourcetype=”stream:http” dest=”192.168.250.70" \*.exe c\_ip=”40.80.148.42" \
> because attacker’s IP — 40.80.148.42

We can find traces of the file in the below image:-\
\


![](https://cdn-images-1.medium.com/max/1000/1\*7ibVtdtGrVgj7kOqQmcoqg.png)

> \
> A)3791.exe

\


> Q)What is the MD5 hash of the executable uploaded?

Web Requests are unlikely to store MD5 hashes of uploaded files,so we instead shift our source type to Windows Sysmon (xmlwineventlog:microsoft-windows-sysmon/operational)

> Query — index=botsv1 sourcetype=”xmlwineventlog:microsoft-windows-sysmon/operational” 3791.exe \
> \| stats values(MD5)

Now,we can go one step further,by grabbing the MD5 Hash,from Sysmon Event

> Query — index=botsv1 sourcetype=”xmlwineventlog:microsoft-windows-sysmon/operational” 3791.exe EventCode=1 \
> \| stats values(MD5)

![](https://cdn-images-1.medium.com/max/1000/1\*X\_JmDqHf8Ew6YiCKOLO7CA.png)

Now,let’s further refine our search,using CommandLine parameter

> Query — index=botsv1 3791.exe CommandLine=3791.exe \
> \| stats values(MD5)\
> A)AAE3F5A29935E6ABCC2C2754D12A9AF0

\


> A)AAE3F5A29935E6ABCC2C2754D12A9AF0

\


> Q)What is the name of the file that defaced the imreallynotbatman.com website?

Using sourcetype as suricata,we can craft the following query:-

> Query — index=botsv1 src=192.168.250.70 sourcetype=suricata dest\_ip=23.22.63.114

From the Web requests generated from the attacker’s IP,we can find 3 unique files:-

![](https://cdn-images-1.medium.com/max/1000/1\*7oRF1n5NSixJF\_tH41UrRg.png)

As witnessed in the beginning of the assignment,a .jpg file had likely defaced the website and “/poisonivy-is-coming-for-you-batman.jpeg” rightly fits that bill

> A)/poisonivy-is-coming-for-you-batman.jpeg

Now,to specify the direction of communication path,using NOT command

> Query — index=botsv1 sourcetype=fgt\_utm “192.168.250.70” NOT dest=”192.168.250.70"

UTM (Unified Threat Management) devices (or next-generation firewalls) often rate or classify various web sites much like standalone web filtering gateways (e.g. Blue Coat). In this case, if we pivot down on category, we see of the nine connections the UTM logged, 3 were to malicious websites. Those sound much more intriguing than the IT sites, so let’s drill down on them.

In this query,we can use **Fortgate Firewall Events Unifies Threat Management(fgt\_utm)**

Now,let’s confirm our hunch

> Query — index=botsv1 sourcetype=fgt\_utm “192.168.250.70” NOT dest=”192.168.250.70" category=”Malicious Websites”

![](https://cdn-images-1.medium.com/max/1000/1\*WdB0lht-5ZpzUacw3t75UQ.png)

> Q)This attack used dynamic DNS to resolve to the malicious IP. What fully qualified domain name (FQDN) is associated with this attack?

In this query,we can make use of fgt\_utm,as sourcetype

> Query — index=botsv1 sourcetype=fgt\_utm “poisonivy-is-coming-for-you-batman.jpeg”

3 logs pop up and let’s expand the first log

We do find the FQDN,in the below image,from the log

![](https://cdn-images-1.medium.com/max/1000/1\*44JqY3dtR2rsTZ5ZJM4gOQ.png)

> A)prankglassinebracket.jumpingcrab.com

\


> Q)What IP address has P01s0n1vy tied to domains that are pre-staged to attack Wayne Enterprises?

For answering this question,we can’t fully make use of Splunk.We take help from other resources like Robtex and ThreatCrowd.

Let’s visit [Robtex](https://www.robtex.com) and query the FQDN \
\


![](https://cdn-images-1.medium.com/max/1000/1\*RN9zLYzfv6m7WfLt4N2qLg.png)

Scrolling down,we can find that 3 IP’s have been tied to domains,in order to attack Wayne Enterprises

![](https://cdn-images-1.medium.com/max/1000/1\*15j2orKekS2UsH5kq8RPdw.png)

Now,for more enumeration of the FQDN,on the [VirusTotal](https://www.virustotal.com/gui/home/upload) platform

![](https://cdn-images-1.medium.com/max/1000/1\*tkvtDwHn-2uJBWcftw3ACw.png)

Searching the IP on VirusTotal brings us:-

![](https://cdn-images-1.medium.com/max/1000/1\*b0UAx7ZkhgV6FcCDWsPUOw.png)

> A)23.22.63.114

\


> Q)Based on the data gathered from this attack and common open source intelligence sources for domain names, what is the email address that is most likely associated with P01s0n1vy APT group

For this,we can use [ThreatCrowd](https://www.threatcrowd.org) tool and reverse search the IP Address — 23.22.63.114

Which gives us the following map layout (similar to Maltego)

![](https://cdn-images-1.medium.com/max/1000/1\*t5xrIxSY8tRoW9q5WLAYpQ.png)

We can find that an email address stands out — [lillianrose@po1s0n1vy.com](mailto:lillianrose@po1s0n1vy.com)

Conducting a whois search on po1s0n1vy.com doesnt pay dividends,as the registrant’s mail address is hidden from public view

We can get the same email address from Maltego,but takes time to extract

> A)[lillianrose@po1s0n1vy.com](mailto:lillianrose@po1s0n1vy.com)

\


> Q)GCPD reported that common TTPs (Tactics, Techniques, Procedures) for the P01s0n1vy APT group if initial compromise fails is to send a spear phishing email with custom malware attached to their intended target. This malware is usually connected to P01s0n1vy’s initial attack infrastructure. Using research techniques, provide the SHA256 hash of this malware.

Searching up P01s0n1vy APT group on MITRE’s site did not give any leads.

From further research,I stumbled upon [threatminer.org](https://threatminer.org),where they display Malware Samples,that are potentiallly cycled by this APT group

![](https://cdn-images-1.medium.com/max/1000/1\*biuyGjbX1bIRv-F77FlXDg.png)

Running this MD5 hash on [VirusTotal](https://www.virustotal.com/gui/home/upload) gave us the following information:-

![](https://cdn-images-1.medium.com/max/1000/1\*qthlqzgVW7M11uBkROb9SQ.png)

Name of Malware file — MirandaTateScreensaver.scr.exe

SHA 256 Hash — 9709473ab351387aab9e816eff3910b9f28a7a70202e250ed46dba8f820f34a8

> A)9709473ab351387aab9e816eff3910b9f28a7a70202e250ed46dba8f820f34a8

\


> Q)What special hex code is associated with the customized malware discussed in the previous question?

Running through VirusTotal’s community section can be gold sometimes.This is where I got the Hex code correlating to this malware file

> A)53 74 65 76 65 20 42 72 61 6e 74 27 73 20 42 65 61 72 64 20 69 73 20 61 20 70 6f 77 65 72 66 75 6c 20 74 68 69 6e 67 2e 20 46 69 6e 64 20 74 68 69 73 20 6d 65 73 73 61 67 65 20 61 6e 64 20 61 73 6b 20 68 69 6d 20 74 6f 20 62 75 79 20 79 6f 75 20 61 20 62 65 65 72 21 21 21

\


> Q)What does this hex code decode to?

Running the hex code on an online converter gives us the following answer:-

> A)Steve Brant’s Beard is a powerful thing. Find this message and ask him to buy you a beer!!!

Task 6 — Ransomware

In this scenario, one of your users is greeted by this image on a Windows desktop that is claiming that files on the system have been encrypted and payment must be made to get the files back. It appears that a machine has been infected with Cerber ransomware at Wayne Enterprises and your goal is to investigate the ransomware with an eye towards reconstructing the attack.&#x20;

If we start with a basic search with the hostname and the index on the specific date that was specified, we can drill down and see which sourcetypes have events that reference that hostname value. The name of the device could be the originator of the event (host) or within the event itself.

> Q)What was the most likely IP address of we8105desk on 24AUG2016?

It appears that we have a pretty robust set of endpoint logs from Sysmon and Windows event logs that reference our host.

> Query — index=botsv1 we8105desk

Now,let’s search for the sourcetypes associated with the desktop we810desk

![](https://cdn-images-1.medium.com/max/1000/1\*j5k4uGL7BZhh\_oPrIIiR8g.png)

Then further click on sourcetype=”XmlWinEventLog:Microsoft-Windows-Sysmon/Operational” and inspect the SourceIP field,where we find:-

![](https://cdn-images-1.medium.com/max/1000/1\*Li9BSlmF19Hd\_bGiff4NIg.png)

Since 192.168.250.100 has the highest percentage of visibility here,we can determine that to be the answer here

> A)192.168.250.100

\


> Q)What is the name of the USB key inserted by Bob Smith?

When analyzing Windows Registry,we can find traces of USB insertion(removable media) being logged here.

USB’s are tagged under a common name titled ‘friendlyname’ on Windows Registry

So,let’s query using winregistry as sourcetype ,with friendlyname as an additional parameter,ordering the data in a tabular manner

> Query — index=botsv1 sourcetype=winregistry friendlyname | table host object data

![](https://cdn-images-1.medium.com/max/1000/1\*2VSGAUY7zm9U6L\_OBV-ZtA.png)

> A)MIRANDA\_PRI

\


> Q)After the USB insertion, a file execution occurs that is the initial Cerber infection. This file execution creates two additional processes. What is the name of the file?

We are all familiar with removable media using drive names,except the C drive.

This will act as a powerful parameter,in our Splunk query

> Query — index=botsv1 sourcetype=XmlWinEventLog:Microsoft-Windows-Sysmon/Operational host=we8105desk “d:\\\” | reverse

The highlighted text is the file that we are looking for!

![](https://cdn-images-1.medium.com/max/1000/1\*f0bl-z0hdHMkerVz\_WZPZQ.png)

> A)Miranda\_Tate\_unveiled.dotm

\


> Q)During the initial Cerber infection a VB script is run. The entire script from this execution, pre-pended by the name of the launching .exe, can be found in a field in Splunk. What is the length in characters of this field?

Let’s construct the following Splunk query,explicitly specifying .exe and sourcing our logs from XmlWinEventLog

> Query — index=botsv1 sourcetype=XmlWinEventLog:Microsoft-Windows-Sysmon/Operational \*.exe \
> \| eval length=len(CommandLine) \
> \| table CommandLine length

![](https://cdn-images-1.medium.com/max/1000/1\*rlIMiTZjYIRXH9y5pRd0dA.png)

We added the eval and the table to our original search but something seems to be off. Can anyone tell me what they might do to improve the output of this search?

There can be Sysmon events that do not have the CommandLine field populated and therefore will return nothing for that field. It is a good idea to use CommandLine=\* in the search to narrow it down to only results that have that field in it. Are there other ways to improve this search?

> Query — index=botsv1 sourcetype=XmlWinEventLog:Microsoft-Windows-Sysmon/Operational \*.exe CommandLine=\* host=we8105desk EventCode=1 | eval length=len(CommandLine) | table CommandLine length | sort — length

We can deduce the length of payload from the below image:-

![](https://cdn-images-1.medium.com/max/1000/1\*GzCCYpAiE1seNuK8ulR\_RA.png)

> A)4490

\


> Q)Bob Smith’s workstation (we8105desk) was connected to a file server during the ransomware outbreak. What is the IP address of the file server?

First,let’s identify the source of Sysmon Events

> Query — index=botsv1 sourcetype=XmlWinEventLog:Microsoft-Windows-Sysmon/Operational host=we8105desk

Let’s double down on the ‘src’ field for values,where we find:-

![](https://cdn-images-1.medium.com/max/1000/1\*1Ma4D8D6cLQVo9296K1MGw.png)

Clicking on we8105desk.waynecorpinc.local and analyzing the corresponding logs from the server,we find the corresponding IP to the server

![](https://cdn-images-1.medium.com/max/1000/1\*Xpks0KA2mvTLoulK7fsI8Q.png)

> A)192.168.250.20

\


> Q)What was the first suspicious domain visited by we8105desk on 24AUG2016?

Let’s target DNS as our sourcetype

> Query — index=botsv1 sourcetype=stream:DNS src=192.168.250.100

Further,let’s refine ‘A’ DNS Records from the recieved logs

> Query — index=botsv1 sourcetype=stream:DNS src=192.168.250.100 record\_type=A

Where we get:-

![](https://cdn-images-1.medium.com/max/1000/1\*JCCvBWCqGRkUqY4TkanOJA.png)

Since we can notice that the workstation user has visited domains like microsoft.com and google.com,these are less likely places for malicious files to be found.This brings us to the following query:-

> Query — index=botsv1 sourcetype=stream:DNS src=192.168.250.100 record\_type=A NOT (query{}=\*.microsoft.com OR query{}=\*.waynecorpinc.local OR query{}=\*.bing.com) | stats count by query{} | sort — 10 count

![](https://cdn-images-1.medium.com/max/1000/1\*Bilf6pfUBPst9On49PZysA.png)

&#x20;Further,let’s refine our query

> Query — index=botsv1 sourcetype=stream:DNS src=192.168.250.100 record\_type=A NOT (query{}=\*.microsoft.com OR query{}=\*.waynecorpinc.local OR query{}=\*.bing.com OR query{}=\*.windows.com OR query{}=\*.msftncsi.com) | stats count by query{} | sort — 10 count

As we look at the list now, we see windows.com and msftncsi.com. A quick whois check on them likely will allow us to add them to our Microsoft whitelist of domains, which gets us down to 5 domains. What else do we have?

Newly blacklisted domains,from log entries

![](https://cdn-images-1.medium.com/max/1000/1\*IjXMZqcBpCUX6jSiq06TuQ.png)

These bring to the last 3 blacklisted domains,where **solidaritedeproximate.org** looks like the real deal

> A)solidaritedeproximite.org

> Q)The malware downloads a file that contains the Cerber ransomware cryptor code. What is the name of that file?

To identify malicious files,we can make use of **fgt\_utm**

> Query — index=botsv1 sourcetype=fgt\_utm src=192.168.250.100 app=”Cerber.Botnet” | reverse

From the resulting query hits,we get the target file

> A)/mhtr.jpg

> Q)What is the parent process ID of 121214.tmp?

We can craft a Splunk query,using XmlWinEventLog as sour sourcetype and CommandLine as an important parameter

> Query — index=botsv1 sourcetype=XmlWinEventLog:Microsoft-Windows-Sysmon/Operational 121214.tmp CommandLine=\* | table \_time CommandLine ProcessId ParentProcessId ParentCommandLine | reverse

![](https://cdn-images-1.medium.com/max/1000/1\*7MDnjDQbAQ\_UZaWCqEOpeA.png)

> A)3968

> Q)Amongst the Suricata signatures that detected the Cerber malware, which signature ID alerted the fewest number of times?

Using Suricata sourcetype

> Query — index=botsv1 sourcetype=suricata alert.signature=\*cerber\*

![](https://cdn-images-1.medium.com/max/1000/1\*6PIpFk3Cy1GaQOAuovc3Dg.png)

> Query — index=botsv1 sourcetype=suricata alert.signature=\*cerber\* | stats count by alert.signature alert.signature\_id | sort count

We get the resulting process id and their parent process id’s in a tabular format

![](https://cdn-images-1.medium.com/max/1000/1\*UIqmZJpcbNPKEFO-GdAwFg.png)

> A)2816763

> Q)The Cerber ransomware encrypts files located in Bob Smith’s Windows profile. How many .txt files does it encrypt?

Initial Query

> Query — index=botsv1 sourcetype=XmlWinEventLog:Microsoft-Windows-Sysmon/Operational host=we8105desk \*.txt

We get over 10 pages of logs

![](https://cdn-images-1.medium.com/max/1000/1\*FT2alPKFCjNxzsevqZjK6Q.png)

> Query — index=botsv1 sourcetype=XmlWinEventLog:Microsoft-Windows-Sysmon/Operational host=we8105desk EventCode=2 TargetFilename=”C:\\\Users\\\bob.smith.WAYNECORPINC\\\\\*.txt” | stats dc(TargetFilename)

> A)406

> Q)How many distinct PDFs did the ransomware encrypt on the remote file server?

PDF format (.pdf)is a great way to filter out resulting queries

> Query — index=botsv1 sourcetype=\*win\* pdf dest=we9041srv.waynecorpinc.local Source\_Address=192.168.250.100 | stats dc(Relative\_Target\_Name)

![](https://cdn-images-1.medium.com/max/1000/1\*zQJqRtthwX2nDvF8zdC5qQ.png)

> A)257

> Q)What fully qualified domain name (FQDN) does the Cerber ransomware attempt to direct the user to at the end of its encryption phase?

As we did earlier,let’s blacklist known good domains,using DNS as sourcetype, to craft our query:-

> Query — index=botsv1 sourcetype=stream:DNS src=192.168.250.100 record\_type=A NOT (query{}=\*.microsoft.com OR query{}=\*.waynecorpinc.local OR query{}=\*.bing.com OR query{}=isatap OR query{}=wpad OR query{}=\*.windows.com OR query{}=\*.msftncsi.com) | table \_time query{} src dest

![](https://cdn-images-1.medium.com/max/1000/1\*3kJyV0w-n9nnasNXNW03GA.png)

\
