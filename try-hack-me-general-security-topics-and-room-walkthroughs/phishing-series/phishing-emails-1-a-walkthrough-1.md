---
description: >-
  Learn the different indicators of phishing attempts by examining actual
  phishing emails.
---

# Phishing Emails - 2: A  Walkthrough

![](../../.gitbook/assets/1.jpg)

Hey blue teamers,

Hope you have combed through the content given in the first Phishing room. Here we are, with the second installment in the series. There is so much to learn!

Room credits go to tryhackme and [heavenraiza](https://twitter.com/heavenraiza)

## Task 1 — Introduction

Now that we covered the basics concerning emails in Phishing Emails 1, let’s dive right into actual phishing email samples.

Each email sample showcased in this room will demonstrate different tactics used to make the phishing emails look legitimate. The more convincing the phishing email appears, the higher the chances the recipient will click on a malicious link, download and execute the malicious file, or even send the prince of some country a wire transfer.

**Warning**: The samples throughout this room contain information from actual spam and/or phishing emails. Proceed with caution if you attempt to interact with any IP, domain, attachment, etc.

## Task 2 - Cancel your PayPal order

The email sample in this task will highlight the following techniques:

* **Spoofed email address**
* **URL shortening services**
* **HTML to impersonate a legitimate brand**

&#x20;                                             ![](https://cdn-images-1.medium.com/max/1000/1\*vaYKoqf3PnqWsMfPmoYjFA.png)

Here are some quick observations about this email sample:

1. This is an unusual email recipient address. This is not the email address associated with the Yahoo account.&#x20;
2. This mismatch should immediately stand out. The sender’s details ([service@paypal.com](mailto:service@paypal.com)) don’t match the sender’s email address ([gibberish@sultanbogor.com](mailto:gibberish@sultanbogor.com)).&#x20;
3. The subject line hints that you made a purchase or a transaction of some sort. If you don’t recall this account, then it will grab your attention. This social engineering tactic is to prompt you to interact with the email with haste.

Now let’s look at the contents of the email body.

**Email Body Text (Image 1):**

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*yq5AZ\_xpawkwK48bWAfdKA.png)

**The second half of the same email body text (Image 2):**

&#x20;                                               ![](https://cdn-images-1.medium.com/max/1000/1\*wIKRcU-bTQOKpCYzSE5iYA.png)

The email body compliments the sender information and subject line. The email was designed as a legitimate email from PayPal.

There aren’t any attachments associated with this email. The only interactive element in this email is the **Cancel the order** button/link.

Let’s investigate that further by reviewing the raw HTML source for the email…

### E**mail Hyperlinks**

&#x20;                                             ![](https://cdn-images-1.medium.com/max/1000/1\*5oOxW-aFRZ-o-xKAPDDcSQ.png)

The link uses URL shortening services. It is not a good idea to click on the link if you don’t know where the link is taking you.

Luckily, there are [online tools](https://wheregoes.com) that we can use to let us know the destination of a shortened URL. &#x20;

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*8oWunN6Iduj\_r90u5y4-XA.png)

Strange. This link redirects to google.com.

**Answer the questions below**

> Q) What phrase does the gibberish sender email start with?

> A)noreply

## Task 3 — Track your package

\
This email sample will highlight the following techniques:

* **Spoofed email address**
* **Pixel tracking**
* **Link manipulation**\


Here are some quick observations about this email sample:

1. The email is tailored to appear that it’s sent from a mail distribution center of some sort.&#x20;
2. The subject line adds to the pretense with a ‘tracking number.’&#x20;
3. The link in the email body matches the subject line.

&#x20;                                          ![](https://cdn-images-1.medium.com/max/1000/1\*BhfRiaXXRxf-mn2WuNLIEw.png)

**Note:** In this email sample, Yahoo blocked the images from automatically loading. Any guesses as to why?

Typically one can hover the cursor over a link to see where the link is pointing to, but in this sample, that technique won’t work because Yahoo disabled links in the email. We can look at the raw source code for the email and find out.

### **Email Hyperlinks**

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*8TEXHDcZsgmeU6xcz\_5UVg.png)

Here we see an image file, and it’s explicitly called **Tracking.png**. These trackers send information back to the spammer’s server.

There are many reasons for spammers to embed tracking pixels (very small images) into their spam emails. To read more about this concept, refer to this post on The Verge [here](https://www.theverge.com/22288190/email-pixel-trackers-how-to-stop-images-automatic-download).

Now we can understand why Yahoo automatically blocked the images in this email. Many email providers do the same.

Back to the hyperlink, the link is pointing to a shady-looking domain. The only distribution center this domain can be associated with is malware, but further analysis is the only way to confirm that.

**Answer the questions below**

> Q) What is the root domain for each URL? Defang the URL.

To defang the URL, we can use the technique used in the previous Phishing room

> A) devret\[.]xyz

## Task 4 — Select your email provider to view the document

This email sample will highlight the following techniques:

* **Urgency**
* **HTML to impersonate a legitimate brand**
* **Link manipulation**
* **Credential harvesting**
* **Poor grammar and/or typos**\


Let’s take a closer look…

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*uW30LKAipElPq4x\_ROb9KQ.png)

Here are some quick observations about this email sample:

1. The email was sent on Thursday, July 15th, 2021.&#x20;
2. A sense of urgency is introduced in this email. Notice that the link to download the fax document expires on the same day.
3. There is an action to perform. In this case, a button to download the fax.

&#x20;                                               ![](https://cdn-images-1.medium.com/max/1000/1\*BVAjDPMK7TqkN4O-UHeRaw.png)

The above image shows the victim is redirected to a page created to pass as OneDrive. Notice that the URL is not anything Microsoft-related.

There are two more links for the victim to interact with. The victim has to click either button to obtain the fax document that is set to expire.

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*4ofrzBhWP-Rnuph9FiluLA.png)

The victim is directed to yet another site. This one was crafted to resemble Adobe. Again, notice the URL. It doesn’t look like it’s related to Adobe.

Also, notice the page title in the tab. It’s called “Share Point Online”, which is a Microsoft product. There are a couple of grammatical errors as well.

The victim has options to sign in with the email provider of their choice.

&#x20;                                            ![](https://cdn-images-1.medium.com/max/1000/1\*0INrxVv3A\_ItBRjAj8Vksw.png)

Our victim chose to log in with Outlook because, per the instructions, “_**To read the document, please enter with the valid email credentials that this file was sent to**_.”; the email was viewed in Outlook.

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*RIeOsusKrza72MVw0gB5OQ.png)

In this sample, we can tell that fake credentials were entered, but even if the victim would have entered valid credentials, the error message would be the same. This scenario happens because the victim is not authenticating to an email provider. Instead, the credentials that were entered now reside on the criminal’s server. The criminal’s objective to harvest credentials has been met.

Lastly, notice more grammatical errors. All this work they put into this, you would think they would run a spell check.

This email sample was obtained from Any Run. If you wish to interact with the email and see the full analysis, refer to the link below.

* **Analysis**: [https://app.any.run/tasks/12dcbc54-be0f-4250-b6c1-94d548816e5c/#](https://app.any.run/tasks/12dcbc54-be0f-4250-b6c1-94d548816e5c/#)

**Answer the questions below**

> Q) This email sample used the names of a few major companies, their products, and logos such as OneDrive and Adobe. What other company name was used in this phishing email?

> A) Citrix

## Task 5 — Please update your payment details

This email sample will highlight the following techniques:

* **Spoofed email address**
* **Urgency**
* **HTML to impersonate a legitimate brand**
* **Poor grammar and/or typos**
* **Attachments**\


Here are some quick observations about this email sample:

1. This email is made to appear that it’s from Netflix Billing, but the sender address is z99@musacombi.online.&#x20;
2. Here is the element of urgency. The account was suspended, so the victim must act quickly.&#x20;
3. There is more of this sense of urgency in the email body.

&#x20;                                                  ![](https://cdn-images-1.medium.com/max/1000/1\*hQWkYlv36cHe1kKdgu7RnQ.png)

Also, notice the different misspellings of the word Netflix. Not sure what was the purpose of that.

Typically, you’ll see this technique when it comes to [typosquatting](https://www.csoonline.com/article/3600594/what-is-typosquatting-a-simple-but-effective-attack-technique.html), but that wasn’t the case here.

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*tjkrGkKHDvzFrpV3QEvaBg.png)

Ok, here is the meat and potatoes of this email. Apparently, the victim needs to open the attachment (PDF) to update their Netflix account.

&#x20;                                                    ![](https://cdn-images-1.medium.com/max/1000/1\*q9q5QsnCCDONclI-iy-8ow.png)

Notice the phone number for ‘Netflix’. At first glance, that is an unusual phone number to send to a US-based victim.

&#x20;                                                     ![](https://cdn-images-1.medium.com/max/1000/1\*6tWYpWelkidkc4r3agc7qg.png)

The attachment contains an embedded link titled ‘Update Payment Account’.

**Answer the questions below**

> Q) What should users do if they receive a suspicious email or text message claiming to be from Netflix?

> A) Forward the message to [phishing@netflix.com](mailto:phishing@netflix.com)

## Task 6 — Your recent purchase

This email sample will highlight the following techniques:

* **Spoofed email address**
* **Recipient is BCCed**
* **Urgency**
* **Poor grammar and/or typos**
* **Attachments**\


Here are some quick observations about this email sample:

1. This email is made to appear that it’s from Apple Support, but the sender’s address is [gibberish@sumpremed.com](mailto:gibberish@sumpremed.com).&#x20;
2. This email wasn’t sent directly to the victim’s inbox but rather BCCed (Blind Carbon Copy). The recipient email looks like another spoofed email to appear as a legitimate Apple email address.&#x20;
3. Here is the element of urgency. Action is required on behalf of the victim.

&#x20;                                           ![](https://cdn-images-1.medium.com/max/1000/1\*kfwSYtVsp1ZYmH7o5EO-3Q.png)

There are a few noticeable typos in both the sender and recipient email addresses: donoreply and payament.

This particular email doesn’t necessarily have an email body. It’s blank. The email simply contains an attachment.

&#x20;                                             ![](https://cdn-images-1.medium.com/max/1000/1\*D7-lvyPxSDRHT3\_rqNHVAg.png)

This file extension may not be familiar to you. A[.DOT](https://www.reviversoft.com/en/file-extensions/dot) file is page layout template files associated with Microsoft Word.

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*gYKFnsem8qxQLtDU6NU35Q.png)

The above image shows what is contained within the attachment. You can see that the file contains a large image to resemble an App Store receipt.

Notice the link contains certain keywords related to Apple: **apps** and **ios**.

**Answer the questions below**

> Q)What does BCC mean?

> A)Blind Carbon Copy

> Q)What technique was used to persuade the victim to not ignore the email and act swiftly?

> A)Urgency

## Task 7 — DHL Express Courier Shipping notice

This email sample will highlight the following techniques:

* **Spoofed email address**
* **HTML to impersonate a legitimate brand**
* **Attachments**

\
Here are some quick observations about this email sample:

1\. The sender’s email doesn’t match the company that is being impersonated, which in this case is DHL.\
2\. The subject line gives the impression that there is a package DHL will ship for you.\
3\. The HTML in the email body was designed to look like it was sent from DHL.

&#x20;                                         ![](https://cdn-images-1.medium.com/max/1000/1\*aRvrzf0zVW\_sw5Wdv8plYQ.png)

Looking at the source code for the email, the link to view the email as a web page doesn’t contain an actual destination URL.

&#x20;                                          ![](https://cdn-images-1.medium.com/max/1000/1\*dA65YUa1S3iul4Jk2afHHw.png)

The only element the victim can interact with within this email is the email attachment, which, in this case, is an Excel document.

&#x20;                                            ![](https://cdn-images-1.medium.com/max/1000/1\*XF3KFRxY-1c\_ecPbqQjFUw.png)

The image below shows what is contained within the attachment.

&#x20;                                             ![](https://cdn-images-1.medium.com/max/1000/1\*8IjGUSafo3E1JzqlKrVc\_g.png)

The attachment runs a payload that throws an error.

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*uUF\_RAgVCc9NoDt394byGQ.png)

**Answer the questions below**

> Q) What is the name of the executable that the Excel attachment attempts to run?

> A)regasms.exe

## Task 8 — Conclusion

In this room, we performed the following activities:-

* Looked at various phishing samples.
* Some of the samples shared similar techniques whereas, others introduced a new tactic for you to see and learn from.
* Understanding how to detect phishing emails takes awareness training.

Additional Resources:

### Additional Resources

* [https://www.knowbe4.com/phishing](https://www.knowbe4.com/phishing)
* [https://www.itgovernance.co.uk/blog/5-ways-to-detect-a-phishing-email](https://www.itgovernance.co.uk/blog/5-ways-to-detect-a-phishing-email)
* [https://cheapsslsecurity.com/blog/10-phishing-email-examples-you-need-to-see/](https://cheapsslsecurity.com/blog/10-phishing-email-examples-you-need-to-see/)
* [https://phishingquiz.withgoogle.com](https://phishingquiz.withgoogle.com)

## Conclusion

Thank you for reading this blog entry and stay tuned as I try to close down more SOC alerts……

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on top of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
