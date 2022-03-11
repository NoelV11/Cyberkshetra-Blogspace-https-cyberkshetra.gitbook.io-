# Linux Fundamentals - Part 3

![](../../.gitbook/assets/24.jpg)

## Task 1 — Introduction

Welcome to part three (and the finale) of the Linux Fundamentals module. So far, throughout the series, you have got hands-on with some fundamental concepts and used some important commands.&#x20;

This room is going to showcase some useful utilities and applications that you are likely to use day-to-day.&#x20;

Room credits go to TryHackMe and [CMNatic](https://twitter.com/CMNatic)

## Task 2 — Deploy Your Linux Machine

## Task 3 — Terminal Text Editors

### **Introducing terminal text editors**

There are a few options that you can use, all with a variety of friendliness and utility. This task is going to introduce you to `nano` but also show you an alternative named `VIM`&#x20;

### **Nano**

It is easy to get started with Nano! To create or edit a file using nano, we simply use&#x20;

> Command — nano \<name\_of\_file>

Once we press enter to execute the command, `nano` will launch! Where we can just begin to start entering or modifying our text. You can navigate each line using the "up" and "down" arrow keys or start a new line using the "Enter" key on your keyboard.

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*O8a4B2qqFyWBN2dagdncZQ.jpeg)

Nano has a few features that are easy to remember & covers the most general things you would want out of a text editor, including:

* Searching for text
* Copying and Pasting
* Jumping to a line number
* Finding out what line number you are on

You can use these features of nano by pressing the “**Ctrl**” key (which is represented as an `^` on Linux) and a corresponding letter. For example, to exit, we would want to press "**Ctrl**" and "**X**" to exit Nano.

### **VIM**

VIM is a much more advanced text editor. Whilst you’re not expected to know all advanced features, it’s helpful to mention it for powering up your Linux skills.

&#x20;                                           ![](https://cdn-images-1.medium.com/max/1000/0\*zymch6UuJ1hLXht\_.png)

Some of VIM’s benefits, albeit taking a much longer time to become familiar with, includes:

* Customizable — you can modify the keyboard shortcuts to be of your choosing
* Syntax Highlighting — this is useful if you are writing or maintaining code, making it a popular choice for software developers
* VIM works on all terminals where nano may not be installed

&#x20;                                           ![](https://cdn-images-1.medium.com/max/1000/1\*DImGCu8Eh3xAhG6BS8ssVg.jpeg)

**Answer the questions below**

> Q)Create a file using Nano

> A)No answer needed

> Q)Edit “task3” located in “tryhackme”’s home directory using Nano. What is the flag?

> A)THM{TEXT\_EDITORS}

![](https://cdn-images-1.medium.com/max/1000/1\*EWTbXjh0G6GoJbMuCMWVxg.jpeg)![](https://cdn-images-1.medium.com/max/750/1\*wcT0\_fgUlimxnz8wu3zGCQ.jpeg)

## Task 4 — General/Useful Utilities

### **Downloading Files**

A pretty fundamental feature of computing is the ability to transfer files. For example, you may want to download a program, a script, or even a picture. Thankfully for us, there are multiple ways in which we can retrieve these files.

We’re going to cover the use of `wget`. This command allows us to download files from the web via HTTP -- as if you were accessing the file in your browser. We simply need to provide the address of the resource that we wish to download. For example, if I wanted to download a file named "myfile.txt" onto my machine, assuming I knew the web address it -- it would look something like this:

```
wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt
```

### **Transferring Files From Your Host — SCP (SSH)**

Secure copy, or SCP, is just that — a means of securely copying files. This command allows you to transfer files between two computers using the SSH protocol to provide both authentication and encryption.

Working on a model of SOURCE and DESTINATION, SCP allows you to:

* Copy files & directories from your current system to a remote system
* Copy files & directories from a remote system to your current system

Provided that we know usernames and passwords for a user on your current system and a user on the remote system. For example, let’s copy an example file from our machine to a remote machine, which I have neatly laid out in the table below:

| Variable                                                    | Value           |
| ----------------------------------------------------------- | --------------- |
| The IP address of the remote system                         | 192.168.1.30    |
| User on the remote system                                   | ubuntu          |
| Name of the file on the local system                        | important.txt   |
| Name that we wish to store the file as on the remote system | transferred.txt |

With this information, let’s craft our `scp` command (remembering that the format of SCP is just SOURCE and DESTINATION)

```
scp http://scp%20important.txt%20ubuntu@192.168.1.30/home/ubuntu/transferred.txt
```

And now let’s reverse this and layout the syntax for using `scp`to copy a file from a remote computer that we're not logged into

| Variable                                                    | Value         |
| ----------------------------------------------------------- | ------------- |
| The IP address of the remote system                         | 192.168.1.30  |
| User on the remote system                                   | ubuntu        |
| Name of the file on the local system                        | documents.txt |
| Name that we wish to store the file as on the remote system | notes.txt     |

The command will now look like the following:

```
scp http://scp%20ubuntu@192.168.1.30/home/ubuntu/documents.txt%20notes.txt
```

### **Serving Files From Your Host — WEB**

Ubuntu machines come pre-packaged with python3. Python helpfully provides a lightweight and easy-to-use module called “HTTPServer”. This module turns your computer into a quick and easy web server that you can use to serve your files, where they can then be downloaded by another computing using commands such as `curl`and `wget`.

Simply, all we need to do is run `python3 -m http.server` to start the module! In the screenshot below, we are serving from a directory called "webserver", which has a single named "file".

&#x20;                                                 ![](https://cdn-images-1.medium.com/max/1000/1\*PgbxMdpN6ATs1OJZH6OYjA.jpeg)

Now, let’s use `wget`to download the file using the computer's IP address and the name of the file. One flaw with this module is that you have no way of indexing, so you must know the exact name and location of the file that you wish to use.

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*u4a6LtSY0CYJAT9MGjcipQ.jpeg)

In the screenshot above, we can see that `wget` has successfully downloaded the file named "file" to our machine. This request is logged by SimpleHTTPServer much as any web server would.

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*Q9XTf-frvDZttDiXVNVDFQ.jpeg)

**Answer the questions below**

> Q)Ensure you are connected to the deployed instance (MACHINE\_IP)

> A)No answer needed

> Q)Now, use Python 3’s “HTTPServer” module to start a web server in the home directory of the “tryhackme” user on the deployed instance.

> A)No answer needed

> Q)Download the file [http://MACHINE\_IP:8000/.flag.txt](http://machine\_ip:8000/.flag.txt) onto the TryHackMe AttackBox

> What are the contents?

> A)THM{WGET\_WEBSERVER}

> Q)Create and download files to further apply your learning — see how you can read the documentation on Python3’s “HTTPServer” module.

> Use Ctrl + C to stop the Python3 HTTPServer module once you are finished.

> A)No answer needed

![](https://cdn-images-1.medium.com/max/750/1\*Y9TkA\_tjpXPu3CyHh3qX2g.jpeg)               ![](https://cdn-images-1.medium.com/max/250/1\*XDk7kww-0wpVVWL9LuygWA.jpeg)![](https://cdn-images-1.medium.com/max/750/1\*MD41EdDXVmTctKYuZhy4Xg.jpeg)

## Task 5 — Processes 101

Processes are the programs that are running on your machine. They are managed by the kernel, where each process will have an ID associated with it, also known as its PID. The PID increments for the order In which the process starts. I.e. the 60th process will have a PID of 60.

### **Viewing Processes**

We can use the friendly `ps` command to provide a list of the running processes as our user's session and some additional information such as its status code, the session that is running it, how much usage time of the CPU it is using, and the name of the actual program or command that is being executed:

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*mYhdi5UUigOYFsZ40E5wXw.jpeg)

To see the processes run by other users and those that don’t run from a session (i.e. system processes), we need to provide **aux** to the `ps` command like:

> Command — ps aux

&#x20;                                                 ![](https://cdn-images-1.medium.com/max/1000/1\*NxyWz-2co3XXTeSR47-V6g.jpeg)

Another very useful command is the top command; top gives you real-time statistics about the processes running on your system instead of a one-time view. These statistics will refresh every 10 seconds, but will also refresh when you use the arrow keys to browse the various rows.

&#x20;                                                 ![](https://cdn-images-1.medium.com/max/1000/1\*Vm0a0ZIVsW6QrwkRQj-3Yg.jpeg)

### **Managing Processes**

You can send signals that terminate processes; there are a variety of types of signals that correlate to exactly how “cleanly” the process is dealt with by the kernel. To kill a command, we can use the appropriately named `kill` command and the associated PID that we wish to kill. i.e., to kill PID 1337, we'd use `kill 1337`.

Below are some of the signals that we can send to a process when it is killed:

* SIGTERM — Kill the process, but allow it to do some cleanup tasks beforehand
* SIGKILL — Kill the process — doesn’t do any cleanup after the fact
* SIGSTOP — Stop/suspend a process

### **How do Processes Start?**

Let’s start by talking about namespaces. The Operating System (OS) uses namespaces to ultimately split up the resources available on the computer to (such as CPU, RAM, and priority) processes. Think of it as splitting your computer up into slices — similar to a cake. Processes within that slice will have access to a certain amount of computing power, however, it will be a small portion of what is available to every process overall.

Namespaces are great for security as it is a way of isolating processes from another — only those that are in the same namespace will be able to see each other.

We previously talked about how PID works, and this is where it comes into play. The process with an ID of 0 is a process that is started when the system boots. This process is the system’s init on Ubuntu, such as **systemd**, which is used to provide a way of managing a user’s processes and sits in between the operating system and the user.

For example, once a system boots and it initializes, **systemd** is one of the first processes that are started. Any program or piece of software that we want to start will start as what’s known as a child process of **systems**.&#x20;

This means that it is controlled by **systemd**, but will run as its own process (although sharing the resources from **systemd**) to make it easier for us to identify and the likes.

&#x20;                                             ![](https://cdn-images-1.medium.com/max/1000/0\*IiuHdnWGeqJw4IR1.png)

### **Getting Processes/Services to Start on Boot**

Some applications can be started on the boot of the system that we own. For example, web servers, database servers, or file transfer servers. This software is often critical and is often told to start during the boot-up of the system by administrators.

In this example, we’re going to be telling the apache webserver to be starting apache manually and then telling the system to launch apache2 on boot.

Enter the use of `systemctl` -- this command allows us to interact with the **systemd** process/daemon. Continuing with our example, systemctl is an easy to use command that takes the following formatting: `systemctl [option] [service]`

For example, to tell apache to start up, we’ll use `systemctl start apache2`. Seems simple enough, right? Same with if we wanted to stop apache, we'd just replace the `[option]` with stop (instead of start like we provided)

We can do four options with `systemctl`:

* Start
* Stop
* Enable
* Disable

### **An Introduction to Backgrounding and Foregrounding in Linux**

Processes can run in two states: In the background and the foreground. For example, commands that you run in your terminal such as “echo” or things of that sort will run in the foreground of your terminal as it is the only command provided that hasn’t been told to run in the background. “Echo” is a great example as the output of echo will return to you in the foreground, but wouldn’t in the background — take the screenshot below, for example.

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/0\*ktM8MPRmHCrVfT1h.png)

Here we’re running `echo "Hi THM"` , where we expect the output to be returned to us like it is at the start. But after adding the `&` operator to the command, we're instead just given the ID of the echo process rather than the actual output -- as it is running in the background.

This is great for commands such as copying files because it means that we can run the command in the background and continue with whatever further commands we wish to execute (without having to wait for the file copy to finish first)

We can do the same when executing things like scripts — rather than relying on the & operator, we can use `Ctrl + Z` on our keyboard to background a process. It is also an effective way of "pausing" the execution of a script or command like in the example below:

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/0\*FK913MerkFdFSz3t.png)

This script will keep on repeating “This will keep on looping until I stop!” until I stop or suspend the process. By using `Ctrl + Z` (as indicated by **T^Z**). Now our terminal is no longer filled up with messages -- until we foreground it, which we will discuss below.

### **Foregrounding a process**

Now that we have a process running in the background, for example, our script “background.sh” which can be confirmed by using the `ps aux`command, we can back-pedal and bring this process back to the foreground to interact with.

&#x20;                                                    ![](https://cdn-images-1.medium.com/max/1000/0\*qH0uHHelO6ySPX1D.png)

With our process backgrounded using either `Ctrl + Z` or the `&` operator, we can use `fg` to bring this back to focus like below, where we can see the `fg` command is being used to bring the background process back into use on the terminal, where the output of the script is now returned to us.

&#x20;                                                       ![](https://cdn-images-1.medium.com/max/1000/0\*n4BYxkUhylK-9a2e.png)

**Answer the questions below**

> Q)Read me!

> A)No answer needed

> Q)If we were to launch a process where the previous ID was “300”, what would the ID of this new process be?

> A)301

> Q)If we wanted to **cleanly** kill a process, what signal would we send it?

> A)SIGTERM

> Q)Locate the process that is running on the deployed instance (MACHINE\_IP). What flag is given?

> A)THM{PROCESSES}

> Q)What command would we use to stop the service “myservice”?

> A)systemctl stop myservice

> Q)What command would we use to start the same service on the boot-up of the system?

> A)systemctl enablemyservice

> Q)What command would we use to bring a previously backgrounded process back to the foreground?

> A)fg

## Task 6 — Maintaining Your System: Automation

### **Cron Jobs**

Users may want to schedule a certain action or task to take place after the system has booted. Take, for example, running commands, backing up files, or launching your favorite programs on, such as Spotify or Google Chrome.

We’re going to be talking about the `cron` process, but more specifically, how we can interact with it via the use of `crontabs` . Crontab is one of the processes that is started during boot, which is responsible for facilitating and managing cron jobs.

A crontab is simply a special file with formatting that is recognized by the `cron` process to execute each line step-by-step. Crontabs require 6 specific values:

| Value | Description                              |
| ----- | ---------------------------------------- |
| MIN   | What minute to execute at                |
| HOUR  | What hour to execute at                  |
| DOM   | What day of the month to execute at      |
| MON   | What month of the year to execute at     |
| DOW   | What day of the week to execute at       |
| CMD   | The actual command that will be executed |

Let’s use the example of backing up files. You may wish to backup “kali’’s “Documents” every 12 hours. We would use the following formatting:

```
0 *12 * * * cp -R /home/kali/Documents /var/backups/
```

An interesting feature of crontabs is that these also support the wildcard or asterisk (`*`). If we do not wish to provide a value for that specific field, i.e. we don't care what month, day, or year it is executed -- only that it is executed every 12 hours, we simply just place an asterisk.

Crontabs can be edited by using `crontab -e`, where you can select an editor (such as Nano) to edit your crontab.

![](https://cdn-images-1.medium.com/max/1000/0\*OVSlUpM\_LFzYUDaO.png)![](https://cdn-images-1.medium.com/max/1000/0\*odIkhaoBj6huEOF8.png)

**Answer the questions below**

> Q)Ensure you are connected to the deployed instance and look at the running crontabs.

> A)No answer needed

> Q)When will the crontab on the deployed instance (MACHINE\_IP) run?

> A)@reboot

## Task 7 — Maintaining Your System: Package Management

### **Introducing Packages & Software Repos**

When developers wish to submit software to the community, they will submit it to an “apt” repository. If approved, their programs and tools will be released into the wild. Two of the most redeeming features of Linux shine to light here: User accessibility and the merit of open source tools.

When using the`ls`command on a Ubuntu 20.04 Linux machine, these files serve as the gateway/registry.

![](https://cdn-images-1.medium.com/max/1000/0\*6yPua8dm\_9f8J580.png)![](https://cdn-images-1.medium.com/max/1000/0\*SSyl-oM5ZKf15pW8.png)

Whilst Operating System vendors will maintain their repositories, you can also add community repositories to your list! This allows you to extend the capabilities of your OS. Additional repositories can be added by using the `add-apt-repository`command or by listing another provider! For example, some vendors will have a repository that is closer to their geographical location.

## Task 8 — Maintaining Your System: Logs

We briefly touched upon log files and where they can be found in Linux Fundamentals Part 1. However, let’s quickly recap. Located in the /var/log directory, these files and folders contain logging information for applications and services running on your system. The Operating System (OS) has become pretty good at automatically managing these logs in a process that is known as “rotating”.

I have highlighted some logs from three services running on a Ubuntu machine:

* An Apache2 web server
* Logs for the fail2ban service, which is used to monitor attempted brute forces, for example
* The UFW service which is used as a firewall

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/0\*ZNLPrjpDsFlq3Cui.png)

These services and logs are a great way in monitoring the health of your system and protect it. Not only that, but the logs for services such as a web server contain information about every single request — allowing developers or administrators to diagnose performance issues or investigate an intruder’s activity. For example, the two types of log files below that are of interest:

* access log
* error log

&#x20;                                                     ![](https://cdn-images-1.medium.com/max/1000/0\*GhboDDXFekwLSNAI.png)

There are, of course, logs that store information about how the OS is running itself and actions that are performed by users, such as authentication attempts.

**Answer the questions below**

> Q)Look for the apache2 logs on the deployable Linux machine

> A)No answer needed

> Q)What is the IP address of the user who visited the site?

> A)10.9.232.111

> Q)What file did they access?

> A)catsanddogs.jpg

## Task 8 — Conclusions & Summaries

Welcome to the end of the Linux Fundamentals module. Your familiarity with Linux will improve as you get to interact with it over time. Linux has the potential to do very powerful things with relative ease (as you have hopefully discovered throughout this module)

To recap, this room introduced you to the following topics:

* Using terminal text editors
* General utilities such as downloading and serving contents using a python webserver
* A look into processes
* Maintaining & automating your system by the use of crontabs, package management, and reviewing logs

## Conclusion

This room allowed me to brush up and revise my command over the Linux CLI and it is a great ground to practice, for those who are new to the Linux game

Thank you for reading this entry. Stay tuned, as I go hunting behind some pcap files out there….

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
