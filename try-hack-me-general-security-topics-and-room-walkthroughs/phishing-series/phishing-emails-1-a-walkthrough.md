---
description: Learn all the components that make up an email.
---

# Phishing Emails - 1: A  Walkthrough

![](<../../.gitbook/assets/1 (1).jpg>)

It was a pretty nice surprise to see that Try Hack Me had dedicated a 5 room series to teach A-Z of everything you need to know about Phishing. Some of these concepts are important and can appear as interview questions. This room is the first one in the series.

So buckle up and start the attached VM!

Room credits go to Try Hack Me and [heavenraiza](https://twitter.com/heavenraiza). Awesome stuff!

## Task 1 — Introduction

[Spam](https://en.wikipedia.org/wiki/Spamming) and [Phishing](https://en.wikipedia.org/wiki/Phishing) are common social engineering attacks. In social engineering, phishing attack vectors can be a phone call, a text message, or an email. As you should have already guessed, our focus is on email as the attack vector.

We all should be somewhat familiar with what spam is. No matter what, these emails somehow find their way into our inboxes.

The first email classified as spam dates back to [1978](https://www.britannica.com/topic/spam), and it’s still thriving today in 2021.

Phishing is a serious attack vector that you, as a defender, will have to defend against.

An organization can follow all the recommended guidelines when it comes to building a layered defense strategy. Still, all it takes is an inexperienced and unsuspecting user within your corporate environment to click on a link or download and run a malicious attachment which may provide an attacker a foothold into the network.

Many products help combat spam and phishing, but realistically these emails still can get through. When they do, as a Security Analyst, you need to know how to analyze these emails to determine if they’re malicious or benign.

In this room, we’ll look at all the components involved with sending emails across the Internet and how to analyze email headers.

## Task 2 — The Email Address

It’s only appropriate to start this room by mentioning the man who invented the concept of emails and made the ‘@’ symbol famous. The person responsible for the contribution to the way we communicate was [Ray Tomlinson](https://en.wikipedia.org/wiki/Ray\_Tomlinson).

The invention of the email dates back to the 1970s for ARPANET. Yep, probably before you were born. Definitely, before I was born. :)

So, what makes up an email address?

* User Mailbox (or Username)
* @&#x20;
* Domain

\
Let’s look at the following email address, [billy@johndoe.com](mailto:billy@johndoe.com).

* The user mailbox is billy
* @ (thanks Ray)
* The domain is johndoe.com

Next, let’s look at the network protocols used to send an email from the sender to the recipient.

**Answer the questions below**

> Q) Email dates back to what time frame?\
> A)1970s

## Task 3 — Email Delivery

A handful of protocols are involved with the “magic” that takes place when you hit SEND in an email client.

By now, you should already know that certain protocols were created to handle specific network-related tasks, such as email.

There are 3 specific protocols involved to facilitate the outgoing and incoming email messages, and they are briefly listed below.

> SMTP (Simple Mail Transfer Protocol) — It is utilized to handle the sending of emails. \
> POP3 (Post Office Protocol) — Is responsible transferring email between a client and a mail server. \
> IMAP (Internet Message Access Protocol) — Is responsible transferring email between a client and a mail server.&#x20;

\
You should have noticed that both POP3 and IMAP have the same definition. But there are differences between the two.

The difference between the two is listed below:

| IMAP                                                                       | POP3                                                                              |
| -------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| Emails are stored on the server and can be downloaded to multiple devices. | Emails are downloaded and stored on a single device.                              |
| Sent messages are stored on the server.                                    | Sent messages are stored on the single device from which the email was sent.      |
| Messages can be synced and accessed across multiple devices.               | Emails can only be accessed from the single device the emails were downloaded to. |

To best illustrate this, see the oversimplified image below:

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*QXQ1njRYyaSl8e9s-Aq8RA.jpeg)

Below is an explanation of each numbered point from the above diagram:

1. Alexa composes an email to Billy (`billy@johndoe.com`) in her favorite email client. After she's done, she hits the send button.
2. The **SMTP** server needs to determine where to send Alexa’s email. It queries **DNS** for information associated with `johndoe.com`.
3. The **DNS** server obtains the information `johndoe.com` and sends that information to the **SMTP** server.
4. The **SMTP** server sends Alexa’s email across the Internet to Billy’s mailbox at `johndoe.com`.
5. In this stage, Alexa’s email passes through various **SMTP** servers and is finally relayed to the destination **SMTP** server.
6. Alexa’s email finally reached the destination **SMTP** server.
7. Alexa’s email is forwarded and is now sitting in the local **POP3/IMAP** server waiting for Billy.
8. Billy logs into his email client, which queries the local **POP3/IMAP** server for new emails in his mailbox.
9. Alexa’s email is copied (**IMAP**) or downloaded (**POP3**) to Billy’s email client.

Lastly, each protocol has its associated default ports and recommended ports. For example, **SMTP** is port 25.

**Answer the questions below**

> Q)What port is classified as Secure Transport for SMTP?

> A)465

> Q) What port is classified as Secure Transport for IMAP?

> A)993

> Q) What port is classified as Secure Transport for POP3?

> A)995

## Task 4 — Email Headers

Great! We know how an email travels from point A to point B and all the protocols involved in the process.

This task is to understand the components of what makes up an email message when it arrives in an inbox.

This understanding is necessary if you wish to analyze potentially malicious emails manually.

Before we begin, we need to understand that there are two parts to an email:

* The email header (information about the email, such as the email servers that relayed the email)
* The email body (text and/or HTML formatted text)

The syntax for email messages is known as the [Internet Message Format](https://datatracker.ietf.org/doc/html/rfc5322) (IMF).

Let’s look at email headers first.

**What do you look for when analyzing a potentially malicious email?**

Let’s start with the following email header fields:

1. From — the sender’s email address
2. Subject — the email’s subject line
3. Date — the date when the email was sent
4. To — the recipient’s email address

\
This is usually clearly visible in any email client. Let’s look at an example of these fields in the below image.

Note: The numbers in the above image correspond to the email header fields bullet list above.

&#x20;                                                 ![](https://cdn-images-1.medium.com/max/1000/1\*r5GfecOlwK8zDC1Nf6-WAQ.png)

**Warning: This is a snippet from an actual email. The email in the below image is from a honeypot Yahoo email address. Don’t engage/interact with the email addresses or IP addresses revealed in this room.**

Another method to obtain the same email header information, and more, is by viewing the ‘raw’ email details.

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*rmxXdQXm5mcPSmZl7\_fvSg.png)

**Note**: Depending on your email client, whether a web client or a desktop app, the steps to view these email header fields will vary, but the concept is the same.

From the above image, there are other email header fields of interest.

> X-Originating-IP — The IP address of the email was sent from (this is known as an X-header)
>
> \
> Smtp.mailfrom/header.from — The domain the email was sent from (these headers are within Authentication-Results)

> Reply-To — This is the email address a reply email will be sent to instead of the From email address

Below is a snippet of the raw message for the email sample.

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*iy\_oBYiZMx-JZX08vSHS6Q.png)

To clarify, in the email in the sample above, the Sender is [newsletters@ant.anki-tech.com](mailto:newsletters@ant.anki-tech.com), but if a recipient replies to the email, the response will go to [reply@ant.anki-tech.com](mailto:reply@ant.anki-tech.com), which is the Reply-To, and NOT to [newsletters@ant.anki-tech.com](mailto:newsletters@ant.anki-tech.com).

Here is an [additional resource](https://mediatemple.net/community/products/all/204643950/understanding-an-email-header) from Media Temple on how to analyze email headers\
**Note**: The questions below are based on the Media Temple KB article.

**Answer the questions below**

> Q) What email header is the same as “Reply-to”?

> A)Return-Path

> Q)Once you find the email sender’s IP address, where can you retrieve more information about the IP?

> A)[http://www.arin.net/](http://www.arin.net)

## Task 5 — Email Body

The email body is the part of the email which contains the text (plain or HTML formatted) the sender wants you to view.

Below is an example of a text-only email.

&#x20;                                                    ![](https://cdn-images-1.medium.com/max/1000/1\*Fekw5K8drUx\_CXIVfsw5Bg.png)

Below is an example of the HTML formatted email.

&#x20;                                                     ![](https://cdn-images-1.medium.com/max/1000/1\*joFJPM5Tyals7qOdpwn8Ww.png)

The above email contains an image (which was blocked by the email client) and embedded hyperlinks.

Viewing an email’s HTML code may vary depending on the webmail client.

A snippet of the HTML code is shown below.

&#x20;                                                       ![](https://cdn-images-1.medium.com/max/1000/1\*a0jgRZ393hnVvHTWQ8LbzQ.png)

Lastly, emails may contain attachments. The same premise applies; you can view an email’s attachment from an email’s HTML format or by viewing the source code.

The following example is an HTML formatted email from “Netflix” with an attachment. The web client is Yahoo!

1. The email body has an image.
2. The email attachment is a PDF document.

&#x20;                                                       ![](https://cdn-images-1.medium.com/max/1000/1\*Wb9bb\_F3b9zf0IO1yPIT8g.png)

Now let’s view this attachment within the source code.

&#x20;                                                       ![](https://cdn-images-1.medium.com/max/1000/1\*VjiP9L\_kab-WrwsV\_vXlaw.png)

From the above example, we can see the headers associated with this attachment:

> Content-Type is application/pdf. \
> Content-Disposition specifies it’s an attachment. \
> Content-Transfer-Encoding tells us it’s base64 encoded. \
> With the base64 encoded data, you can decode it and save it to your machine.

**Warning**: When interacting with attachments, proceed with caution and make sure you don’t double-click an email’s attachment by accident.

**Answer the questions below**

> Q) In the above screenshots, what is the URI of the blocked image?

> A)[https://i.imgur.com/LSWOtDI.png](https://i.imgur.com/LSWOtDI.png)

> Q)In the above screenshots, what is the name of the PDF attachment?

> A)Payment-updateid.pdf

> Q)In the attached virtual machine, view the information in email2.txt and reconstruct the PDF using the base64 data. What is the text within the PDF?

On the desktop, we find a folder named ‘Email Samples’ and there is a file within, titled email2.txt

Opening it, we find that the mail is encoded in base64 format

&#x20;                                                           ![](https://cdn-images-1.medium.com/max/1000/1\*tXuwDaLVqywgDwKcH8\_g0Q.jpeg)

Our task is to decode it to plaintext. Let’s use CyberChef for the task. Copy-paste the encoded input and select “from base64”.Proceed to decode and save the blob as Decode.pdf (**you can use any file name, but what matters is saving the file in PDF format**)\
Open the download.pdf and read the flag.

> A)\<Flag is undisclosed>

&#x20;                                                            ![](https://cdn-images-1.medium.com/max/1000/1\*gGRzTeitxqcpzX0DKCTzww.jpeg)

## Task 6 — Types of Phishing

Now that we covered the general concepts regarding emails and how they travel from sender to recipient, we can now talk about how this method of communication is used for nefarious purposes.

Different types of malicious emails can be classified as one of the following:

> Spam — unsolicited junk emails sent out in bulk to a large number of recipients. The more malicious variant of Spam is known as MalSpam.
>
> \
> Phishing — emails sent to a target(s) purporting to be from a trusted entity to lure individuals into providing sensitive information.&#x20;

> Spear phishing — takes phishing a step further by targeting a specific individual(s) or organization seeking sensitive information.&#x20;

> Whaling — is similar to spear phishing, but it’s targeted specifically to C-Level high-position individuals (CEO, CFO, etc.), and the objective is the same.&#x20;

> Smishing — takes phishing to mobile devices by targeting mobile users with specially crafted text messages.&#x20;

> Vishing — is similar to smishing, but instead of using text messages for the social engineering attack, the attacks are based on voice calls.&#x20;

When it comes to phishing, the modus operandi is usually the same depending on the objective of the email.

For example, the objective can be to harvest credentials, and another is to gain access to the computer.

Below are typical characteristics phishing emails have in common:

* The **sender email name/address** will masquerade as a trusted entity (email spoofing)
* The email subject line and/or body (text) is written with a sense of urgency or uses certain keywords such as **Invoice, Suspended**, etc.&#x20;
* The email body (HTML) is designed to match a trusting entity (such as Amazon)
* The email body (HTML) is poorly formatted or written (contrary from the previous point)
* The email body uses generic content, such as Dear Sir/Madam.&#x20;
* Hyperlinks (oftentimes uses URL shortening services to hide its true origin)
* A malicious attachment posing as a legitimate document

**Reminder**: When dealing with hyperlinks and attachments, you need to be careful not to accidentally click on the hyperlink or the attachment.

Hyperlinks and IP addresses should be ‘defanged’. You can read more about this technique [here](https://www.ibm.com/docs/en/sqsp/32.0?topic=SSBRUQ\_32.0.0/com.ibm.resilient.doc/install/resilient\_install\_defangURLs.htm).

Analyze the email titled email3.eml within the virtual machine and answer the questions below.

> Note: Alexa is the victim, and Billy is the analyst assigned to the case. Alexa forwarded the email to Billy for analysis.

**Answer the questions below**

> Q) What trusted entity is this email masquerading as?

Taking a look at the 'From' field, it looks as if it is encoded in UTF format. So our first approach was to decode it

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*V\_GwQWqfBQ4g7pKkYhUnfw.jpeg)

That approach did not suffice

After running around in circles, I decided to take a chance with Base64 decoding.

&#x20;                                                     ![](https://cdn-images-1.medium.com/max/1000/1\*OmWS7uuimkjNqMtwes1mAw.jpeg)

Well, that worked out well

> A) Home Depot

> Q)What is the sender’s email?

> A) [support@teckbe.com](mailto:support@teckbe.com)

> Q)What is the subject line?

Let’s attempt decoding the subject line, using Base64 Decoding\
Well, that worked out well

&#x20;                                                        ![](https://cdn-images-1.medium.com/max/1000/1\*pYuTqyhFJiFtukdW6F1uqA.jpeg)

> A)Order Placed : Your Order ID 0D2321657089291 Placed Successfully

> Q)What is the URL link for — CLICK HERE? (Enter the defanged URL)

This was considerably harder, as the URL found from the HTML Source code doesn't match the pattern

So, let’s consult the help of Cyber Chef. Select (Find/Replace) and (Defang URL) recipes, to decode

Enter =3D in the Find field and click on bake

&#x20;                                                            ![](https://cdn-images-1.medium.com/max/1000/1\*OOZ8LDmqBIrrovjh\_B3SiA.jpeg)

> A)hxxp\[://]t\[.]teckbe\[.]com/p/?j3EOo=wFcEwFHl6EOAyFcoUFVTVEchwFHlUFOo6lVTTDcATE7oUE7AUET

## Task 7 — Conclusion

Before ending this room, you should know what BEC (Business Email Compromise) means.

A BEC is when an adversary gains control of an internal employee’s account and then uses the compromised email account to convince other internal employees to perform unauthorized or fraudulent actions.

**Tip**: You should be familiar with this term. I have heard this question asked before in a job interview.

Within this room, we covered the following:

* What makes up an email address?
* How an email travels from sender to recipient.
* How to view the source code of an email header.
* How to view the source code of an email body.&#x20;
* Understand the pertinent information we should obtain from an email we’re analyzing.
* Some common techniques attackers use in spam and phishing email campaigns.

In the upcoming Phishing Analysis series, we’ll look at samples of various common techniques used in phishing email campaigns, along with tools to assist us with analyzing an email header and email body.

Next room in this module: Phishing Emails 2

**Answer the questions below**

> Q) What is BEC?

> A) Business Email Compromise

## Conclusion

Being a cybersecurity student, this is a topic that is hot right now, with the advent of the raging war. I am glad to have collected more information about Email header analysis, while having brushed up my knowledge on different phishing schemes and how to differentiate a phishing mail, from an authentic one

Good work from TryHackMe, for having released this 5 room series. I am raring to do the other rooms as well!&#x20;

Thank you for reading this blog and stay tuned as I try to close down more SOC alerts……

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by giving it a clap!
