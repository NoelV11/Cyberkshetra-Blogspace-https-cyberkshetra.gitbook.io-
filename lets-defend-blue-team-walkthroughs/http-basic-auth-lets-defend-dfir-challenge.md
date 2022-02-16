# HTTP Basic Auth:Let's Defend DFIR Challenge

&#x20;                                            ![](https://cdn-images-1.medium.com/max/1000/1\*H1rhWTgN9396jHzWCFn0qA.png)

Hello, blue teamers! Welcome to this latest blog post, as I document my methodology of solving the [HTTP Basic Auth](https://app.letsdefend.io/dfir/dfir/http-basic-auth/) challenge on Let’s Defend. Let’s go hunting after this .pcap file

## Gist of Challenge

> We got some log indicates the attacker, can you gathering information from pcap file?

> Log file: [https://app.letsdefend.io/download/downloadfile/webserver.em0.zip](https://app.letsdefend.io/download/downloadfile/webserver.em0.zip)\
> Pass: 321

## **Questions**

> Q)How many HTTP GET requests are in pcap?

You can solve this question in two ways

Navigate to Statistics ->HTTP ->Requests,where we can find:-

![](https://cdn-images-1.medium.com/max/1000/1\*F38xpfe43Voabjajk5t4yg.png)

or

Enter the following query on the search tab — http.request.method==”GET”

Where we find the following GET request packets

![](https://cdn-images-1.medium.com/max/1000/1\*Uv-5PTGOvbZmX9TQdRp2tw.png)

> A)5

> Q)What is the server operating system?

When analyzing one of the HTTP GET request packets, from the .pcap file, we can find the following information:-

Web Server version\
OpenSSL Version\
Server Distro Name

![](https://cdn-images-1.medium.com/max/1000/1\*JZ2o-e3otR8kTyRV0QSqvw.png)

> A)FreeBSD

> Q)What is the name and version of the web server software?

It is visible from the User-Agent section of the packet&#x20;

> A)Apache/2.2.15

> Q)What is the version of OpenSSL running on the server?

> A)OpenSSL/0.9.8n

> Q)What is the client’s user-agent information?

![](https://cdn-images-1.medium.com/max/1000/1\*FmA14pDg4z1mXHCn7fzt8g.png)

> A){Lynx/2.8.7rel.1 libwww-FM/2.14 SSL-MM/1.4.1 OpenSSL/0.9.8n}

> Q)What is the username used for Basic Authentication?

Hunting through the GET requests, we find this username and password entered for authentication purposes

![](https://cdn-images-1.medium.com/max/1000/1\*ejDaFd\_ZxhxpugG597odYA.png)

> A)webadmin

> Q)What is the user password used for Basic Authentication?

> A)W3b4Dm1n

## Conclusion

This challenge was a breeze!

Thank you for reading this entry. Stay tuned, as I go hunting behind some pcap files out there....

## Your opinion matters

My audience has a voice. Feel free to reach out to me, on my socials (links are on the side of this page) for any queries to be addressed. Dropping a sweet message would make my day

Let your opinion about this write-up be known, selecting any one of the emojis below!
