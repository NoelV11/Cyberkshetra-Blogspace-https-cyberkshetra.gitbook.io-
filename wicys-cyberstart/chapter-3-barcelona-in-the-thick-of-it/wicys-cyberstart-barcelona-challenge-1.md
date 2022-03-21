---
description: XOR Decoding
---

# WiCYS CyberStart (Barcelona) Challenge 1

![](../../.gitbook/assets/CS.png)

Hello, fellow Cyberstart gamers!

Having touched base 3 on our CyberStart journey, in Barcelona, it’s time again to solve some security challenges. We are handed an overview of the challenges on the horizon.

&#x20;                                               ![](https://cdn-images-1.medium.com/max/1000/1\*aZ9FSwZc8g\_QpnUAas8T3w.jpeg)



## Briefing L03 C01

### **Hextraordinary**

&#x20;                                                  ![](https://cdn-images-1.medium.com/max/1000/1\*kRCv\_0Gxekh8jqgxV4cqMw.jpeg)

> Intern, the agency have been in contact with a rival hacker to a new, secretive gang of hackers who goes by the name “ROXy”. She specializes in short, cryptic, hard to decipher secret codes.

> ROXy is willing to work with us… if we can prove we’re as smart as she is. Before she’ll hand over any information, she’s given us a code to break first.

> If you can help us break this code, we’ll gain an important new informant.

> **Tip**: The flag is the secret code.

We are provided with the codes, from ROXy in this email

&#x20;                                           ![](https://cdn-images-1.medium.com/max/1000/1\*mVfOrdB0eZop55jEcDgbYQ.jpeg)

Codes — 0xB105F00D and 0xAAA8400A

## Hex or XOR?

By looking at the syntax of codes, it is evident that they are of XOR type. Let’s see if they equate to something on an [online XOR calculator](https://xor.pw/#)

Proceed to insert them in the given blanks — input A and B and click on Calculate XOR

&#x20;                                              ![](https://cdn-images-1.medium.com/max/1000/1\*6iFC\_Pngj07UuC\_fBycqmA.jpeg)

The resultant value is = 1badb007

Since it was asked to get the code in 0x form, let’s append it to the start of the code and submit it

Turns out it was the correct answer.

### Scoreboard

![](<../../.gitbook/assets/screenshot (8).png>)

Onward ahoy to the next challenge!

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*w8-6TI22-E-onxe7psNE\_w.jpeg)
