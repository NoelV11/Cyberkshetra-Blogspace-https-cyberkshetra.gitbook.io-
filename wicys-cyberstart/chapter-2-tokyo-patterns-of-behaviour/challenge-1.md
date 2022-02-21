# Challenge 1

![](../../.gitbook/assets/CS.png)

Hello fellow Cyberstart gamers!

Having touched base 2 on our CyberStart journey, it's again time to solve some security challenges. We are handed an appreciation letter and an overview of the challenges on the horizon

&#x20;                                                      ![](https://cdn-images-1.medium.com/max/1000/1\*3mPeR74izswagoOtEnfvwQ.jpeg)

## Briefing L02 C01

### 610enC0de’d Password

&#x20;                                                       ![](https://cdn-images-1.medium.com/max/1000/1\*4gbBA7QXcRUuLe8Zo-CAXQ.jpeg)

> Agents believe they have found a server belonging to a gang called the Yakoottees. If we can get access to it who knows what information we can gather on them! So far the Yakoottees have been very successful hiding their activities by encoding everything they do. We’ve found their server but don’t have the password and so can’t login. Can you help, intern?

> **Tip:** Login to the server to get the flag.

Proceeding to the challenge, we are met with this terminal screen

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*MzoSoJq4yfokBYQ-SjZBxg.jpeg)

At first glance, this text looks like hex encoding. Our job is to now decode it, to gain access to Yakoottees’ server

For that, I would suggest you use this [resource](https://string-functions.com/hex-string.aspx). Others were not able to decode the hex-encoded text and you will see why. Copy-paste the hex code and decode it

This is our output

&#x20;                                                     ![](https://cdn-images-1.medium.com/max/1000/1\*NwfC9YbtsdOuHd3dSwMsTQ.jpeg)

The cleartext looks a bit messy, doesn't it? Let’s clean it up

From our research, it is found that ‘?’ is represented as \x63 in hex code

&#x20;                                                      ![](https://cdn-images-1.medium.com/max/1000/1\*\_cQvy5c1w6D8\_BaHlj7CiQ.jpeg)

I was able to find just 2 instances of \x63 but did not make the output any cleaner

From the jumbled decoded text, we can decipher the password (by removing question marks)

> Password = 4f1b252055

Using it to login onto the server

&#x20;                                                         ![](https://cdn-images-1.medium.com/max/1000/1\*3U3m0eUb5gaJIe4nKLxEpg.jpeg)

> Flag — cA3drVNxuDvgmcN5gs5i

We are in and the challenge is conquered!

Coupled with that, we have 500 points on the scoreboard. Onward Ahoy!

&#x20;                                                           ![](https://cdn-images-1.medium.com/max/1000/1\*rzV4898WyqgWaS26N2iPZQ.jpeg)

