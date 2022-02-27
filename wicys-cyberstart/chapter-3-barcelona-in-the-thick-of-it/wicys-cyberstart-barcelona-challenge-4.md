# WiCYS CyberStart (Barcelona) Challenge 4

![](../../.gitbook/assets/CS.png)

## Briefing L03 C04

### **The Final Countdown**

&#x20;                                                 ![](https://cdn-images-1.medium.com/max/1000/1\*uQk7yudW-X\_Fi2t2C6btTA.jpeg)

> The main tourism website for Barcelona has been hacked. They’ve devised a program that changes the content of the website based on a timer. You can imagine the confusion this has been causing the sites visitors! Can you figure out how we can get the secret code to stop this program from running?

> **Tip**: The characters at the 5 URLs change quickly, but computers can be far quicker than humans, especially when getting data!

Proceeding to the challenge, we are given a set of links

&#x20;                                                           ![](https://cdn-images-1.medium.com/max/1000/1\*UVEmYL2DsCQrJnyOpyHRgg.jpeg)

**So what's the objective?**

Clicking on each of the 5 links (under the timing section) gives us 5 different strings, which together form a passphrase.

The challenge here is that the strings need to be collected in under 10 seconds and inserted as parameters in the validation link

**How do we collect the strings effectively?**

cURL to the rescue again!

Steps:-

Step 1 - curl all the links to get the strings we want (do not list each of them in separate lines!)

Why? — we are aiming to collect data from the websites. In this case, we are using curl to aid us.

```
curl https://roambarcelona.com/clock-pt1?verify=Na2Q%2BeqhSP5hTRLDwpTNoA%3D%3D https://roambarcelona.com/clock-pt2?verify=Na2Q%2BeqhSP5hTRLDwpTNoA%3D%3D https://roambarcelona.com/clock-pt3?verify=Na2Q%2BeqhSP5hTRLDwpTNoA%3D%3D https://roambarcelona.com/clock-pt4?verify=Na2Q%2BeqhSP5hTRLDwpTNoA%3D%3D
```

It should look something like this. Keep this ready, before the timer is up

&#x20;                                                    ![](https://cdn-images-1.medium.com/max/1000/1\*-PgUwqgy7WzSIGbcsegOmA.jpeg)

Step 2 - Take the validation link and open it in another browser. Clear the string parameter and leave it empty

```
https://roambarcelona.com/get-flag?verify=Na2Q%2BeqhSP5hTRLDwpTNoA%3D%3D&string=
```

#### Execution Time!

Run the curl command (when timer resets to 10) and quickly insert the generated passphrase from the CLI to the end of the validation string

Voila, you get your flag!

&#x20;                                                   ![](https://cdn-images-1.medium.com/max/1000/1\*5pzAWWqUhWnXIMhiD0EqlA.jpeg)

> Flag — wh1te\_Ro$E                                                &#x20;

Final point count - 2400                     &#x20;

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*ybCqWyAdZdsehSS1o80IKA.png)

Well fellow gamers, my internship time is up, as I am on a free CyberStart license (up to 3 levels only). It was a great time to complete challenges (both easy and challenging) and draft writeups for the same. Hope you enjoyed the time spent on CyberStart.

Until then, goodbye. Stay connected on my socials (given at the top of this page). Dropping a sweet message would make my day
