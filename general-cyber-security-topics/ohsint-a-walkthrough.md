# OhSint:A Walkthrough

![](../.gitbook/assets/IW.png)

​Hello readers,welcome to this segment of my blog,as I guide you to solve the [OhSint](https://tryhackme.com/room/ohsint) Room,hosted on TryHackMe.This room is a lot of fun!

## Task 1 - OhSint

What information can you possible get with just one photo?​![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fq8Yzn5Spn9wAtMsEuJ0B%2Fuploads%2FiR4O0rSfGdhTQL6kT7fB%2F1.png?alt=media\&token=10d4b42e-4566-4b6a-97bc-bcdf9ae12a84)

​Looks familiar doesn't it?

Firstly, we may be able to scrape some metadata off this image, so let’s run it on Exiftool, a CLI utility on Kali Linux

`Command — exiftool Windows.jpg`

Which gives us,

![](https://cdn-images-1.medium.com/max/1000/1\*247Fa6UnwesLjE\_\_FXmEkA.png)

So, we’ve got a starting point,i.e OWoodflint

My mind went on overdrive from here. So I decided to run this name/username on Maltego and see what happens from there

![](https://cdn-images-1.medium.com/max/1000/1\*FaciZcaEC7OsdaR9jiwvYQ.png)

NOTE: The search was conducted using ‘All transforms’

Oh sweet! We have a Github, Twitter & WordPress page to investigate. Let’s head to Twitter first, to [OWoodfl1nt’s](https://twitter.com/owoodflint?lang=en) page, where we find:-

![](https://cdn-images-1.medium.com/max/1000/1\*dzz19\_A2L-mofA0q5elU2Q.png)

Well, this was easy ain't it?

> Q)What is this users avatar of?

> A)cat

> Which city is this person in?

Poking around the tweets posted by fl1nt, did not provide us any clue towards this question. Well I did find this from one of his tweets

![](https://cdn-images-1.medium.com/max/1000/1\*iULMVV-quL7vDgv6ugw4NQ.png)

Let’s keep this for later

Now let’s focus our attention on his [Github](https://github.com/OWoodfl1nt) page, where he has one repository. Its README file is gold, though

![](https://cdn-images-1.medium.com/max/1000/1\*FfIZeY1mMwjltl32FOY2Mw.png)

He is from London!

> A)London

> Q)Whats the SSID of the WAP he connected to?

Connecting this question with the earlier clue (BBSSID), we took guidance from the Twitter tweet reply thread to try our luck at [Wigle.net](https://wigle.net), to trace it.

**NOTE**: It requires signup

Heading to the ‘Advanced Search’ feature and putting in the BSSID gives us the following result

![](https://cdn-images-1.medium.com/max/1000/1\*CDd1qUdcwoZKwmj5phhlQQ.png)

> A)UnileverWiFi

> Q)What is his personal email address?

This information was present on the Github repository README file

> A)[OWoodflint@gmail.com](mailto:OWoodflint@gmail.com)

> Q)What site did you find his email address on?

> A)Github

> Q)Where has he gone on holiday?

Heading to flint’s [WordPress blog](https://oliverwoodflint.wordpress.com), we are met with this:-

![](https://cdn-images-1.medium.com/max/1000/1\*GnC3PZPUvkFW6yxrDd2How.png)

> A)New York

> Q)What is this persons password?

This was a bit of a tough find. Combing through the Twitter page and Github commits history/comments gave us no clue.

Well, the source page of WordPress has been guilty of holding passwords in the past. In this case, it was not an exception

> A)pennYDr0pper.!

**NOTE**:Never insert your password/password files as cleartext comments in the source code of a website.Use a password manager instead

## Conclusion

Ever since I took part in CSAM Investigation rings to find criminals on the Dark Web,I have never understated the importance of OSINT in everyday life,to solve simple problems.A person's pghone or email address is now a query away from being found

Thank you for reading this blog entry and stay tuned as I try to close down more SOC alerts……

My audience has a voice. Feel free to reach me out on my socials, in case of any queries to be addressed. Let your opinion about this write-up be known by selecting any one of the emojis below!
