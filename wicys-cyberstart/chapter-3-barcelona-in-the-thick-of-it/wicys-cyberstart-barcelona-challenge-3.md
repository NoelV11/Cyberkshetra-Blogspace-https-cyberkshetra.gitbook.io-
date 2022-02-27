# WiCYS Cyberstart (Barcelona) Challenge 3

![](../../.gitbook/assets/CS.png)

## Briefing L03 C03 <a href="#a5cd" id="a5cd"></a>

### Off Balance <a href="#afd4" id="afd4"></a>

&#x20;                                           ![](https://miro.medium.com/max/761/1\*9dDt2LLhthNxkCJMV5Ps8w.jpeg)

> We’re hot on the heels of catching this cyber gang but the closer we get the more damage they try to inflict onto the Barcelona tourism industry! This time, they’ve hacked into a large international bank’s mobile application. Customers of the bank are complaining they can’t see their current balance. Intern, help customers retrieve their balances so they can continue to spend their money during their well-earned holidays!
>
> **Tip**: Bypass the calculator lock to get the flag.

We can find this banking app —with sections for Recent Transactions, Payments, and Account Balances. The third section of the app is where we have a problem.



&#x20;    ![](https://miro.medium.com/max/830/1\*y3UdcxiqRHRbNtVX5uazZw.jpeg)![](https://miro.medium.com/max/826/1\*5TWvWFllp0aBpeMWLDjKYA.jpeg)



&#x20;                                   ![](https://miro.medium.com/max/764/1\*dI01OZ7\_MYhjc1gOJlfhsQ.jpeg)  &#x20;

So our objective is to find the contents of the Balances page

How do we go about that?

Open the source code and head over to the 'Network' section, where we find the following web paths.

&#x20;                              ![](https://miro.medium.com/max/1400/1\*536YZJB\_Ju2hIIutGTBhgg.jpeg)

As seen in the picture /get-balances path is currently facing a 404 error and is unreachable. The rest are perfectly fine.

Extend ‘/get-balances to get more information about the path

&#x20;                              ![](https://miro.medium.com/max/435/1\*-PKcgLVwWWAn4AAx28BxCQ.jpeg)

To test the connection, let's cURL the connection to /get-transactions. Use your Kali’s CLI interface for this

```
Command - curl -s https://cloudninebank.com/get-transactions
```

&#x20;                                    ![](https://miro.medium.com/max/520/1\*p7-JcaPZlg4LTwyx6JZKHA.jpeg)

A token is required as additional data to the URL. This can be found in the Payload section of the Inspect Element. Let’s now test a working web path.I chose /get-payments

Adding it to our curl command, we get:-

```
curl -d “CNcsmXX5d50ZQCG5Us4twDi18awV” -s https://cloudninebank.com/get-balances
```

&#x20;                                        ![](https://miro.medium.com/max/788/1\*rWZAHiDKy1iU\_pn6Agd7mA.jpeg)

Now, let's proceed to test /get-balances

What we get is a “Resource not found” reply.

&#x20;                                         ![](https://miro.medium.com/max/788/1\*oM15lPQ\_TP3wqscID3Gk6w.jpeg)

See, the stark difference

## Flag Capture <a href="#9a34" id="9a34"></a>

Seeing no other tweaks to make, now let’s curl the main website

```
curl -d “token=CNcsmXX5d50ZQCG5Us4twDi18awV” -s https://cloudninebank.com
```

&#x20;                                       ![](https://miro.medium.com/max/710/1\*XPwZIipGHSU\_u1xTOecJdQ.jpeg)

Hey, hey what do we notice here?\
Instead of get-balances entry, we find a path get-accounts. Let’s curl that instead, using the token value

&#x20;                                      ![](https://miro.medium.com/max/788/1\*xp12mQV8TJfDDkx2SWpX2w.jpeg)

As you notice, the flag is present towards the bottom

> Flag — postD4ta\_w1zard

Submit it and onward ahoy to the next challenge.2100 points racked up on the scoreboard as well!

&#x20;                                         ![](https://miro.medium.com/max/524/1\*3Cqq7IAVKSbFXN42E8cQqw.jpeg)
