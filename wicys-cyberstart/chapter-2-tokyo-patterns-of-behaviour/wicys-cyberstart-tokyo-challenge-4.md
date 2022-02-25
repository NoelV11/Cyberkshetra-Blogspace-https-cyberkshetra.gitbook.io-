---
description: Web Login vulnerability
---

# WiCYS CyberStart (Tokyo) Challenge 4

![](../../.gitbook/assets/CS.png)

## Briefing L02 C04

### **Start-Up Troubles**

&#x20;                                           ![](https://cdn-images-1.medium.com/max/1000/1\*JJGNV9X\_CY2bVV\_0EUTKRQ.jpeg)

> A successful new start-up that sells electric scooters has discovered a handful of their customers’ accounts have been hacked! And guess who we believe might be behind it? Yep, you’ve guessed it, the Yakoottees. Having only just entered the market and keen to maintain their otherwise excellent reputation, this business needs our help to run a security audit of their login system. Can you spot any security holes?

> **Tip**: Successfully login to get the flag.

We come across this login page, belonging to the Zip Zap Rides startup

&#x20;                                           ![](https://cdn-images-1.medium.com/max/1000/1\*xtyDN3V9\_owgZEngN\_NZ\_g.jpeg)

The manual says that there is a vulnerability on this website. Let’s hunt that down!

I took three approaches to solve this, each more complex than the next one.

## Approach 1 — Editing the HTML code

If you look closely, there are 4 parameters whose values we need to know. These are email, password, submittedEmail, and SubmittedPassword

&#x20;                                               ![](https://cdn-images-1.medium.com/max/1000/1\*gq9ikzURWBFKOI\_2Qp1ljg.jpeg)

Since the values were not present, I tried to manipulate the source code, inserting custom values

![](https://cdn-images-1.medium.com/max/1250/1\*-NJOhSfxnuuKOigdpSOfUg.jpeg)![](https://cdn-images-1.medium.com/max/500/1\*HPx4s8Q1xhNTysSi4OzNhQ.jpeg)

This did not work, as I was repeatedly changing comments one after the other, to get the login page to work

## Approach 2 — SQL Injection

Having no email address (from the company) to use in the email field, it was worth a try to try payloads from this [Github repository](https://github.com/payloadbox/sql-injection-payload-list) and spray it on the password section

That approach did not work as well

## Approach 3 — Using the web console

Right. This was the way out.

Since the console had come in handy in the previous challenge, let’s make use of it.

Right click ->Console

We can observe that the parameters for login were ‘email’ and ‘password’.Let’s try querying it against the console

This is what we get:-

&#x20;                                                  ![](https://cdn-images-1.medium.com/max/1000/1\*bLI96tchg7CM2d-bT-mb6A.jpeg)

We get what we have been looking for!

> Login page credentials

> Email — bonita@zip-zap-rides.com

> Password — letmein

## Flag Capture

Use it to log in and we get the flag

> Flag — pgHGwHToGfFE2MC4BF1A

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*8qNXK4RAZPPzBqIFKgRLNA.jpeg)

We have racked up 1200 points on the leaderboard. It’s time to bid farewell to the Tokyo base (especially when it gave us our hardest challenge yet) and set base somewhere else. Let’s see where our CyberStart journey takes us.

Onward to the next challenge!
