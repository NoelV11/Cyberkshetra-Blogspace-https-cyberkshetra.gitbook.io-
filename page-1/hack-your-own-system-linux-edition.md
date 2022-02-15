# Hack your own system-Linux Edition

Hello there,

Welcome to Noel's Cyberkshetra Blogspace,where I document my cyber security learning and journey,as I make my way towards achieving a &#x20;

Linux OS is the go-to target for any aspiring hacker. Whether it be configuring the pam.d file or cracking the root password, the possibilities are endless. Ask any hacker and they would reply saying Linux is their favorite OS to intrude to.

Let’s discuss what makes Linux so revered.

* Root Authentication-Before a normal user downloads a file off the internet, or plays around with the system configuration, care is taken to get the root user’s authentication to carry out the task. The only snag is that the normal user or intruder gets a certain ’n’ chances to brute-force the password, before the account gets locked.
* Centralized Package Management-Unlike Windows, where drivers and software can be downloaded from shoddy, third-party websites, Linux distributions download required software packages from a dedicated package managers, such as RPM, yum etc.
* Less Audience-With the dwindling amount of users, by the year, the chances of being hit by a virus is remote.

Coming to the point, we will see how the root user’s password can be cracked, to gain access to the system. Note that the demonstration is done on CentOS distribution, installed on VMware.

Step 1-Boot up the Linux OS , by starting the machine, on the VM

Step 2-After loading screen, the user is presented with two options to use the installed Linux distribution. Press ‘e’ on the first option.

![](https://miro.medium.com/max/1400/1\*sqsPsCLYjDmzoC1z4PYitw.png)

The grub menu

Step 3-The screen depicting the grub parameters will now load up.The user should edit the line starting with the character ‘f45’.

![](https://miro.medium.com/max/60/1\*tStgAplg7r\_zpc5fGidnjQ.png?q=20)![](https://miro.medium.com/max/788/1\*tStgAplg7r\_zpc5fGidnjQ.png)

The rd.break command is used to interrupt the boot process, while the control is given to the kernel.

Step 4-The required editing of parameters ,is shown below. The combination of Ctrl+X must be performed, to enforce single user mode.

![](https://miro.medium.com/max/60/1\*NOgfPqn-0IzzmH8ZvvFWJg.jpeg?q=20)![](https://miro.medium.com/max/788/1\*NOgfPqn-0IzzmH8ZvvFWJg.jpeg)

Step 5-In emergency mode (without graphical support),the user will need to have the read-write permissions to edit the root password ,on the file system. Further, the user needs to specify the name of the user,whose password needs to be reset.

![](https://miro.medium.com/max/60/1\*kto4Ql\_3H0PSgCHv6a-tJA.png?q=20)![](https://miro.medium.com/max/788/1\*kto4Ql\_3H0PSgCHv6a-tJA.png)

Each command is completed by pressing ‘Enter’

The new password entered are not visible ,which is a method called shadowing the password. You don’t want others to peer over your shoulders to see the password, do you?

The working behind the touch /.autorelabel command is interesting.This command creates a hidden file called .autorelabel, under the root’s directory. After exit command , the system reboots and SELinux (provider of process level security) detects this file and relabels all the contents ,with the appropriate SELinux contexts (combination of user, role ,type of file ,sensitivity and category).

So there you go ,a fool-proof method to re-enter your system, in case you forget your master password. Hacking into your own system is more like it.

Well, thank you, for spending your precious time ,in digesting this article and I mean it.

Stay tuned and I will be back with more.
