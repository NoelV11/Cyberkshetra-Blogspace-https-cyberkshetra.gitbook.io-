---
description: >-
  A simple challenge, involving changing of a URL destination, to find a hidden
  webpage.
---

# WiCYS CyberStart (Tokyo) Challenge 3

![](../../.gitbook/assets/CS.png)

Briefing L02 C03

### **Traffic Jam**

&#x20;                                           ![](https://cdn-images-1.medium.com/max/1000/1\*ZdD30FVVNMOIM1RTgretvA.jpeg)

> Can you believe it, we think the Yakoottees are now planning to disrupt the flow of traffic in a major city! We need to find the URL of a forum they’re using to communicate with each other. Can you figure out what the URL is?

> **Tip**: Find the url of the forum to get the flag.

Visiting the Yakoottees’ website, this is what we find:-

&#x20;                                     ![](https://cdn-images-1.medium.com/max/1000/1\*eUYbmTvQBbbCTKFVFLLY0A.jpeg)

While visiting each page, it has different URLs, which is evident in the images below. This is very important to observe. Keep it in mind

![](https://cdn-images-1.medium.com/max/1000/1\*XpsP3jONXxSxdo3UZWDytw.jpeg)![](https://cdn-images-1.medium.com/max/1000/1\*ZuZ-LzUHQfhApvvchOG3xQ.jpeg)

&#x20;                                     ![](https://cdn-images-1.medium.com/max/750/1\*Br-G2IAFOb65PX9NjGnYQg.jpeg)

Putting this into a tabular form, we have:-

| Prefix    | Section of the Website |
| --------- | ---------------------- |
| company   | About                  |
| my-routes | Cycling Maps           |
| contact   | Contact Us             |

In each case, a prefix is attached to the main URL (trafficdisruptors.com)

## Flag Capture

To get a full list, we can observe the source code of the webpage. Sometimes analyzing this is akin to a gold mine

&#x20;                                             ![](https://cdn-images-1.medium.com/max/1000/1\*0geoF5geKMMBZRUDziVg0A.jpeg)

So we can observe that “forum” has a prefix — my-chat

Appending it to the main URL, we get the final URL, targeting the forum page

> ([https://my-chat.trafficdisruptors.com/312324494](https://my-chat.trafficdisruptors.com/312324494))

Upon pressing enter, we capture the flag

&#x20;                                                ![](https://cdn-images-1.medium.com/max/1000/1\*bZBhhTA1UAIUiJSeJUOIgg.jpeg)

> Flag — WiNlHGVYPAm0iGig5lhu

Contents of the forum page:-

&#x20;                                                 ![](https://cdn-images-1.medium.com/max/1000/1\*lcbNltfQ28IFdRu2HiICgA.jpeg)

The challenge is conquered and we have racked up 1000 points on the scoreboard. Way to go!

&#x20;                                                  ![](https://cdn-images-1.medium.com/max/1000/1\*gN2IWknJhcRD7Uv\_dZLHbQ.jpeg)

