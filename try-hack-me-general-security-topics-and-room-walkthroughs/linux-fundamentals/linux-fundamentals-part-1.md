---
description: Power up your Linux skills!
---

# Linux Fundamentals - Part 1

![](<../../.gitbook/assets/4 (1).jpg>)

Hello, aspiring blue teamers,

This article walks you through working on Linux and basic commands that can help get your work done. Try Hack Me has released a 3 part series on Linux Fundamentals and [this room](https://tryhackme.com/room/linuxfundamentalspart1) is the first one in the collection.

For all those who want to get a hang of how Linux works, open the Virtual Machine provided by Try Hack Me and follow along

Room credits go to TryHackMe and [CMNatic](https://twitter.com/CMNatic)

**NOTE**: To demonstrate this room, I have used Debian, a flavor of Linux

## Task 1 — Introduction

Welcome to the first part of the “Linux Fundamentals” room series. You’re most likely using a Windows or Mac machine, both are different in visual design and how they operate. Just like Windows, iOS, and macOS, Linux is just another operating system and one of the most popular in the world —  powering smart cars, android devices, supercomputers, home appliances, enterprise servers, and more.

We’ll be covering some of the histories behind Linux and then eventually starting your journey of being a Linux wizard! This room will have you:

* Running your very first commands in an interactive Linux machine in your browser
* Teaching you some essential commands used to interact with the file system
* Introduce you to how users and groups work on Linux (and what this means for us as penetration testers)

## Task 2 — A bit of background on Linux

### **Where is Linux Used?**

It’s fair to say that Linux is a lot more intimidating to approach than Operating System’s (OSs) such as Windows. Both variants have their own advantages and disadvantages. For example, Linux is considerably much more lightweight and you’d be surprised to know that there’s a good chance you’ve used Linux in some form or another every day! Linux powers things such as:

* Websites that you visit
* Car entertainment/control panels
* Point of Sale (PoS) systems such as checkout tills and registers in shops
* Critical infrastructures such as traffic light controllers or industrial sensors

### Flavors of Linux

The name “Linux” is an umbrella term for multiple OSs that are based on UNIX (another operating system). Thanks to UNIX being open-source, variants of Linux come in all shapes and sizes — suited best for what the system is being used for.

For example, Ubuntu & Debian are some of the more commonplace distributions of Linux because it is so extensible. I.e. you can run Ubuntu as a server (such as websites & web applications) or as a fully-fledged desktop. For this series, we’re going to be using Ubuntu.

> _**Note**:Ubuntu Server can run on systems with only 512MB of RAM_

Similar to how you have different versions of Windows (7, 8, and 10), there are many different versions/distributions of Linux.

**Answer the questions below**

Research: What year was the first release of a Linux operating system?

> A)1991

## Task 3 — Interacting With Your First Linux Machine (In-Browser)

## Task 4 — Running Your First few Commands

As we previously discussed, a large selling point of using OS’ such as Ubuntu is how lightweight they can be. This, of course, doesn’t come without its disadvantages, where for example, often there is no GUI (Graphical User Interface) or what is also known as a desktop environment that we can use to interact with the machine (unless it has been installed). A large part of interacting with these systems is using the “Terminal”.

The “Terminal” is purely text-based and is intimidating at first. However, if we break down some of the commands, after some time, you quickly become familiar with using the terminal!

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*CKFmUron\_-gry7vJS2e1Cw.jpeg)

Let’s get started with two of the first commands which I have broken down in the table below:

| Command | Description                                                |
| ------- | ---------------------------------------------------------- |
| echo    | Output any text that we provide                            |
| whoami  | Find the identity of the user we're currently logged in as |

Demonstration of each command:

&#x20;                                                      ![](https://cdn-images-1.medium.com/max/1000/1\*grv\_SrM5zD8Aj2c-FmHSyw.jpeg)

**Answer the questions below**

> Q)If we wanted to output the text “**TryHackMe**”, what would our command be?

> A)echo “**TryHackMe**”

> Q)What is the username of who you’re logged in as on your deployed Linux machine?

> A)tryhackme

&#x20;                                                      ![](https://cdn-images-1.medium.com/max/1000/1\*nZIMyr5FQ0\_NopOstOeGYg.jpeg)

## Task 5 — Interacting With the Filesystem!

So far we’ve only covered the “**echo**” and “**whoami**” commands. In this task, we’re going to be learning the commands that enable you to interact with the filesystem. Have a look at the table below:-

| Command | Description                                                   |
| ------- | ------------------------------------------------------------- |
| ls      | List all files present in a directory                         |
| cd      | Change / Traverse directories                                 |
| cat     | Read the contents of a file                                   |
| pwd     | Find the path of directory, that you are currently located at |

NOTE: To not overwhelm you with information, I will give you the background information needed to perform these commands

* The /home directory (located in the main directory (/) contains all files that are specific to the user you are logged in as currently (i.e Kali, in my case)

### Listing Files in Our Current Directory (ls)

Before we can do anything such as finding out the contents of any files or folders, we need to know what exists there in the first place. This can be done using the “ls” command (short for listing)

> Command — ls

&#x20;                                                           ![](https://cdn-images-1.medium.com/max/1000/1\*1q3XxCUNoAq0Fr2rLhSsOQ.jpeg)

In the screenshot above, we can see there are the following directories:

* bin
* etc
* games and so on

> _Pro tip: You can list the contents of a directory without having to navigate to it by using **ls** and the name of the directory. I.e. `ls Pictures`_

### Changing Our Current Directory (cd)

Now that we know what folders exist, we need to use the “**cd**” command (short for **c**hange **d**irectory) to change to that directory.&#x20;

> Say if I wanted to open the “Downloads” directory in my home folder— I’d do&#x20;

> Command — **cd Downloads**&#x20;

I have broken this down into 6 segments (traversing back and forth to /home/kali/Downloads), from the main directory (/)

&#x20;                                                     ![](https://cdn-images-1.medium.com/max/1000/1\*L8Vw1pJbBXEOfk9fuqtrlg.jpeg)

### Outputting the Contents of a File (cat)

Whilst knowing about the existence of files is great — it’s not all that useful unless we’re able to view the contents of them.

&#x20;We’re going to talk about simply seeing the contents of text files using a command called “**cat”.**

In the screenshot below, you can see how I have combined the use of “cd” to list the files within a directory called “Downloads”:

&#x20;                                                      ![](https://cdn-images-1.medium.com/max/1000/1\*v1tKUYqSCjtAAnQUXw9V6w.jpeg)

We’ve applied some knowledge from earlier in this task, to do the following:

1. Used “**ls**” to let us know what files are available in the “Downloads” folder of this machine. In this case, it is called “Text”.
2. We have then used `cat Text` to output the contents of this file, where the contents are "Text inside a file inside titled Text”

> _Pro tip: You can use `cat` to output the contents of a file within directories without having to navigate to it by using **cat** and the name of the directory. I.e. `cat /home/kali/Downloads/Text`_

### Finding out the full Path to our Current Working Directory (pwd)

You’ll notice as you progress through navigating your Linux machine, the name of the directory that you are currently working in will be listed in your terminal.

It’s easy to lose track of where we are on the filesystem exactly, which is why I want to introduce “**pwd**”. This stands for **p**rint **w**orking **d**irectory.

Using the example machine from before, we are currently in the “Downloads” folder — but where is this exactly on the Linux machine’s filesystem? We can find this out using this “pwd” command like within the screenshot below:

&#x20;                                                         ![](https://cdn-images-1.medium.com/max/1000/1\*iy11kOeGeWMxLu5KWKDrqg.jpeg)

**Let’s break this down:**

1. We already know we’re in “Downloads” thanks to our terminal, but at this point, we have no idea where “Documents” is stored so that we can get back to it easily in the future.
2. I have used the “**pwd**” (**p**rint **w**orking **d**irectory) command to find the full file path of this “Downloads” folder.
3. We’re helpfully told by Linux that this “Documents” directory is stored at “/home/kali/Downloads” on the machine — great to know!

**Answer the questions below**

> Q)On the Linux machine that you deploy, how many folders are there?

> A)4

> Q)Which directory contains a file?

> A)folder4

> Q)What is the contents of this file?

> A)Hello World

> Q)Use the cd command to navigate to this file and find out the new current working directory. What is the path?

> A)/home/tryhackme/folder4

&#x20;                                                             ![](https://cdn-images-1.medium.com/max/1000/1\*fg7nE8UCTLSNHURSLTogwg.jpeg)

## Task 6 — Searching for Files

Although it doesn’t seem like it so far, one of the redeeming features of Linux is truly how efficient you can be with it. With that said, you can only be as efficient as you are familiar with it of course. As you interact with OSs such as Ubuntu over time, essential commands like those we’ve already covered will start to become muscle memory.

One fantastic way to show just how efficient you can be with systems like this is using a set of commands to quickly search for files across the entire system that our user has access to. No need to consistently use `cd` and `ls` to find out what is where. Instead, we can use commands such as `find` to automate things like this for us!

### Using Find

The find command is fantastic in the sense that it can be used both very simply or rather complex depending upon what it is you want to do exactly.

It becomes a headache when we’re having to look through every single one just to try and look for specific files. We can use `find` to do just this for us!

Let’s start simple and assume that we already know the name of the file we’re looking for — but can’t remember where it is exactly! In this case, we’re looking for “Text.txt”

If we remember the filename, we can simply use&#x20;

> Command — find / -name Text.txt -type f

> Parameters:-

> / — search in current directory

> \-name = specify name of file

> \- type = type/format of file.In this case,it is a simple text file.Hence we applied ‘f’ as an argument

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*bUA\_unabI3JqOd1Q54tfKg.jpeg)

“Find” has managed to _find_ the file — it turns out it is located in home/kali/Downloads— sweet. But let’s say that we don’t know the name of the file, or want to search for every file that has an extension such as “.xlsx”. Find let’s us do that too!

We can simply use what’s known as a wildcard (\*) to search for anything that has .xlsx at the end. In our case, we want to find every .xlsx file that’s in our current directory. We will construct a command such as:

> Command — find -name \*.xlsx

&#x20;                                                       ![](https://cdn-images-1.medium.com/max/1000/1\*MBGDbwR5ch3UPH3fUYFybQ.jpeg)

Find command has managed to _find_:

1. “Example.xlsx” is located within the “Downloads” folder (in kali user’s directory)
2. “Example2.xlsx” located within “kali”
3. “Example3.xlsx” located within the “Documents” folder

That wasn’t so tough huh!

### Using Grep

Another great utility that is a great one to learn about is the use of `grep`. The `grep` command allows us to search the contents of files for specific values that we are looking for.

Let’s take the example of “rockyou.txt” (the largest dataset of breached passwords) and grep a few commands, as a demonstration

> Command — grep “cyber\*” rockyou.txt

> Meaning = Display all passwords starting with the word “cyber”&#x20;

> Grep symbol used — \*

&#x20;                                                       ![](https://cdn-images-1.medium.com/max/1000/1\*VgZ86Mo4BOZ6yoR5XdrJwg.jpeg)

> Command — grep “^noel” rockyou.txt

> Meaning = Display all passwords having “noel” as a part of the password

> Grep symbol used — ^

&#x20;                                                          ![](https://cdn-images-1.medium.com/max/1000/1\*v-rLz\_LNyYde4zYUzTFGUg.jpeg)

> Command — grep “noel$” rockyou.txt

> Meaning = Display all passwords ending with the word “noel”

> Grep symbol used — $

&#x20;                                                        ![](https://cdn-images-1.medium.com/max/1000/1\*n0gb5QEB\_uLrX3G7RFgEgg.jpeg)

> Command — grep “^noel$” rockyou.txt

> Meaning = Display all passwords having “noel” in between as a word

> Grep symbol used — ^ and $

&#x20;                                                       ![](https://cdn-images-1.medium.com/max/1000/1\*4a\_5gkYhcAgwkPCptlQ8Xg.jpeg)

**Answer the questions below**

> Q)Use grep on “access.log” to find the flag that has a prefix of “THM”. What is the flag?

> A)THM{ACCESS}

> Q)And I still haven’t found what I’m looking for!

> A)No answer needed

&#x20;                                                      ![](https://cdn-images-1.medium.com/max/1000/1\*MgjS9LDWead8gGOAJ7qSAw.jpeg)

## Task 7 — An Introduction to Shell Operators

Linux operators are a fantastic way to power up your knowledge of working with Linux. There are a few important operators that are worth noting. We’ll cover the basics and break them down accordingly to bite-sized chunks.

At an overview, I’m going to be showcasing the following operators:

Let’s cover these in a bit more detail.

### Operator “&”

This operator allows us to execute commands in the background. For example, let’s say we want to copy a large file. This will take quite a long time and will leave us unable to do anything else until the file is successfully copied.

The “&” shell operator allows us to execute a command and have it run in the background (such as this file copy) allowing us to do other things!

&#x20;                                                           ![](https://cdn-images-1.medium.com/max/1000/1\*3wctRoGrXoioM5WI0Hb9XA.jpeg)

> Command — whoami & touch Example.txt

> Meaning = Display the identity of the user,you are currently logged in as and create a file titled ‘Example.txt’

### Operator “&&”

This shell operator is a bit misleading in the sense of how familiar is to its partner “&”. Unlike the “&” operator, we can use “&&” to make a list of commands to run for example `command1 && command2`. However, it's worth noting that `command2` will only run if `command1` was successful. This applies to the other chained commands&#x20;

&#x20;                                                             ![](https://cdn-images-1.medium.com/max/1000/1\*j7cllotd4KAx1YH5SauDXA.jpeg)

> Command — touch Password && echo “TryHackMe%” >> Password && ls && cat Password && reboot

> Meaning/Sequence of events:-

> Create a file titled ‘Password’

> Display the string ‘TryHackMe%’

> Enter that string into the newly created ‘Password’ file

> Show the contents of Password file

> Reboot the Linux system

### Operator “>”

This operator is what’s known as an output redirector. What this essentially means is that we take the output from a command we run and send that output to somewhere else.

Let’s say we wanted to enter a message “Dummy Information”, to a file titled ‘Text.txt’. We can run:

> Command — echo “Dummy Information” > Text.txt

&#x20;                                                      ![](https://cdn-images-1.medium.com/max/1000/1\*SaF9AL1VAci99Anqg4mawQ.jpeg)

### Operator “>>”

This operator is also an output redirector like in the previous operator (`>`) we discussed. However, what makes this operator different is that rather than overwriting any contents within a file, for example, it instead just puts the output at the end.

Following on with our previous example where we have the file “Text.txt” that has the contents of “Dummy”. If were to use echo to add “Information” to the file using the `>` operator, the file will now only have "Dummy" and not "Information".

The `>>` operator allows to append the output to the bottom of the file — rather than replacing the contents like so:

&#x20;                                                         ![](https://cdn-images-1.medium.com/max/1000/1\*21lVCMoA39hOHBzO9vHSNQ.jpeg)

> Command — echo “Dummy” >> Text.txt

Enters the input “Dummy” into the file Text.txt

> echo “Information” >> Text.txt

Appends the input “Dummy” into the file Text.txt

**Answer the questions below**

> Q)If we wanted to run a command in the background, what operator would we want to use?

> A)&

> Q)If I wanted to replace the contents of a file named “passwords” with the word “password123”, what would my command be?

> A)echo password123 > passwords

> Q)Now if I wanted to add “tryhackme” to this file named “passwords” but also keep “passwords123”, what would my command be

> A)echo tryhackme >> passwords

> Q)Now use the deployed Linux machine to put these into practice

> A)No answer needed

&#x20;                                                     ![](https://cdn-images-1.medium.com/max/1000/1\*uwI3CpmEqUd5LEcjCyMlEw.jpeg)

## Task 8 — Conclusions

Nice work on getting to this stage! We covered quite a bit for your first interactions with Linux.

To quickly recap, we’ve covered the following:

* Understanding why Linux is so commonplace today
* Interacting with your first-ever Linux machine!
* Ran some of the most fundamental commands
* Had an introduction to navigating around the filesystem & how we can use commands like find and grep to make finding data even more efficient!
* Power up your commands by learning about some of the important shell operators.

Take some time to have a play-around in this room. When you feel a little bit more comfortable, progress onto [Linux Fundamentals Part 2](https://tryhackme.com/jr/linuxfundamentalspart2/)

## Conclusion

This room allowed me to brush up and revise my command over the Linux CLI and it is a great ground to practice, for those who are new to the Linux game

Thank you for reading this entry. Stay tuned, as I go hunting behind some pcap files out there….

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
