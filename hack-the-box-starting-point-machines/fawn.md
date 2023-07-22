---
description: 'OS Type: Unix'
cover: ../.gitbook/assets/1 (17).png
coverY: 0
---

# Fawn

Let's start the challenge, by connecting to openvpn through Terminal and spawning the machine, to obtain the target machine's IP Address

We find that the dynamic IP Address assigned to the machine is - 10.129.251.118

> Q1) What does the 3-letter acronym FTP stand for?

> A1) file transfer protocol

> Q2)  Which port does the FTP service listen on usually?

> A2) 21

> Q3) What is the command we can use to send an ICMP echo request to test our connection to the target?

> A3) ping

> Q4) What acronym is used for the secure version of FTP?

> A4) SFTP

Also known as Secure FTP / FTP Secure. It is powered by SSH (indicating the 'S' in SFTP) and is operational via Terminal, using SSH Keys

> Q5) From your scans, what version is FTP running on the target?

First, let's conduct an Nmap scan on the target. Adding the -sV flags will be beneficial to uncover the version of the FTP Server running on the machine

Command - nmap \<Machine IP> -sV -p 21 -vv

&#x20;                                ![](<../.gitbook/assets/image (5).png>)&#x20;

The version of the FTP Server here is vsftpd 3.0.3

> A5) vsftpd 3.0.3

> Q6) From your scans, what OS type is running on the target?

Oops, i revealed the answer above!

> A6) Unix

> Q7) What is the command we need to run in order to display the 'ftp' client help menu?

> A7)  ftp -h

You can run the command on your terminal later, as we can logon to the FTP Server on this machine. This command will be helpful.

> Q8) What is username that is used over FTP when you want to log in without having an account?

> A8) anonymous

An anonymous user does not require a password to login, but the bane is that certain commands cannot be run and privileges may be restricted on the server to the user.

Let's log onto the server meanwhile

&#x20;                                    ![](<../.gitbook/assets/image (7).png>)

> Q9) What is the response code we get for the FTP message 'Login successful'?

As seen from the login attempt, we were met with a status '230' code. This indicates that we were able to login successfully

> A9) 230

> Q10) There are a couple of commands we can use to list the files and directories available on the FTP server. One is dir. What is the other that is a common way to list files on a Linux system.

> A10) ls

> Q11)  What is the command used to download the file we found on the FTP server?

Let's check the files present here

&#x20;                                      ![](<../.gitbook/assets/image (1).png>)

Our beloved flag file is present!

Knowledge Nugget Time

| File Management Commands | Funcitonality                      | Usage           |
| ------------------------ | ---------------------------------- | --------------- |
| get                      | Download a file off the FTP Server | get \<filename> |
| put                      | Upload a file to the FTP Server    | put \<filename> |

As quoted in the question, we need to download the flag.txt file from the server, so running the command [`get flag.txt`](#user-content-fn-1)[^1]on the server interface would be apt

> A11) get

The file gets downloaded to the home or Downloads directory of the host VM. A manual check would be required.

> Q12) Submit root flag

> A12) \<Your flag>

Let's meet at the next machine to be pwned. Thank you, I hope the walkthrough was engaging and useful to you

&#x20;                                       ![](<../.gitbook/assets/image (6).png>)

[^1]: 
