# Google Dorking: A Walkthrough

![](../.gitbook/assets/70.png)

Hello readers.Welcome to this segment of Noel's blog entries,as I learn and solve Try Hack Me's 'Google Dorking' Room.It's a pretty fun concept to learn and implement in real life,as you hunt down for research papers and so on.

Room credits go to [CMNatic](https://twitter.com/CMNatic).Cheerio!

## Task 1 - Ye Ol' Search Engine

Google is arguably the most famous example of “Search Engines”, I mean who remembers Ask Jeeves? ~~_shudders_~~

Now it might be rather patronising explaining how these “Search Engines” work, but there’s a lot more going on behind the scenes then what we see. More importantly, we can leverage this to our advantage to find all sorts of things that a wordlist wouldn’t. Researching as a whole - especially in the context of Cybersecurity encapsulates almost everything you do as a pentester. [MuirlandOracle](https://tryhackme.com/p/MuirlandOracle) has created a [fantastic room](https://tryhackme.com/room/introtoresearch) on learning the attitudes towards how to research, and what information you can gain from it exactly.

"Search Engines" such as Google are huge indexers – specifically, indexers of content spread across the World Wide Web.

These essentials in surfing the internet use “Crawlers” or “Spiders” to search for this content across the World Wide Web, which I will discuss in the next task

Questions:-

> Q)Roger dodger!

> A)Mark as completed

## Task 2 - **What are Crawlers and how do They Work?**

These crawlers discover content through various means. One is by pure discovery, where a URL is visited by the crawler and information regarding the content type of the website is returned to the search engine. There are a lot of information modern crawlers scrape — but we will discuss how this is used later. Another method crawlers use to discover content is by following any URLs found from previously crawled websites. Much like a virus in the sense that it will want to traverse/spread to everything it can.

**Let’s Visualise Some Things…**

The diagram below is a high-level abstraction of how these web crawlers work. Once a web crawler discovers a domain such as **mywebsite.com**, it will index the entire contents of the domain, looking for keywords and other miscellaneous information

![](https://cdn-images-1.medium.com/max/1000/1\*VlyYb474Iui93dmkAs5jXw.png)

In the diagram above, “**mywebsite.com**” has been scraped as having the keywords “Apple” “Banana” and “Pear”. These keywords are stored in a dictionary by the crawler, who then returns these to the search engine i.e. Google. Because of this persistence, Google now knows that the domain “**mywebsite.com**” has the keywords “Apple”, “Banana”, and “Pear”. As only one website has been crawled, if a user was to search for “Apple”…“**mywebsite.com**” would appear. This would result in the same behavior if the user was to search for “Banana”. As the indexed contents from the crawler report the domain as having “Banana”, it will be displayed to the user.

As illustrated below, a user submits a query to the search engine of “Pears”. Because the search engine only has the contents of one website that has been crawled with the keyword of “Pears” it will be the only domain that is presented to the user.

![](https://cdn-images-1.medium.com/max/1000/1\*viESdR0GZfOWIcH9DizZGw.png)

However, as we previously mentioned, **crawlers attempt to traverse, termed as crawling, every URL and file that they can find!** Say if “**mywebsite.com**” had the same keywords as before (“Apple”, “Banana” and “Pear”), but also had a URL to another website “**anotherwebsite.com**”, the crawler will then attempt to traverse everything on that URL (**anotherwebsite.com**) and retrieve the contents of everything within that domain respectively.

This is illustrated in the diagram below. The crawler initially finds “**mywebsite.com**”, where it crawls the contents of the website — finding the same keywords (“Apple”, “Banana” and “Pear”) as before, but it has additionally found an external URL. Once the crawler is complete on “**mywebsite.com**”, it’ll proceed to crawl the contents of the website “**anotherwebsite.com**”, where the keywords (“Tomatoes”, “Strawberries” and “Pineapples”) are found on it. The crawler’s dictionary now contains the contents of both “**mywebsite.com**” and “**anotherwebsite.com**”, which is then stored and saved within the search engine.

![](https://cdn-images-1.medium.com/max/1000/1\*7bubkPJguFanMan2mPM8xw.png)

### **Recapping**

So to recap, the search engine now knows two domains that have been crawled:\
1\. mywebsite.com\
2\. anotherwebsite.com

As illustrated below:

![](https://cdn-images-1.medium.com/max/1000/1\*9te7KdWva3\_Md4xxHX5eYg.png)

Now that the search engine has some knowledge about keywords, say if a user was to search for “Pears” the domain “**mywebsite.com**” will be displayed — as it is the only crawled domain containing “Pears”:

![](https://cdn-images-1.medium.com/max/1000/1\*4h3pF7dA1r8RauyQG64feQ.png)

This is great…But imagine if a website had multiple external URLs (as they often do!) That’ll require a lot of crawling to take place. There’s always the chance that another website might have similar information as that another website crawled — right? So how does the “Search Engine” decide on the hierarchy of the domains that are displayed to the user?

In the diagram below in this instance, if the user was to search for a keyword such as “Tomatoes” (which websites 1–3 contain) who decides what website gets displayed in what order?

![](https://cdn-images-1.medium.com/max/1000/1\*9nMU3orDSSiI2VorDQndeA.png)

A logical presumption would be that website 1 -> 3 would be displayed…But that’s not how real-world domains work and/or are named.

Questions:-

> Q)Name the key term of what a “Crawler” is used to do

> A)Index

> Q)What is the name of the technique that “Search Engines” use to retrieve this information about websites?

> A)Crawling

> Q)What is an example of the type of content that could be gathered from a website?

> A)Keywords

### Task 3 — Enter Search Engine Optimization

### S**earch Engine Optimisation**

Search Engine Optimisation or SEO is a prevalent and lucrative topic in modern-day search engines. So much so, that entire businesses capitalize on improving a domain's SEO “ranking”. At an abstract view, search engines will “prioritize” those domains that are easier to index. There are many factors in how “optimal” a domain is — resulting in something similar to a point-scoring system.

To highlight a few influences on how these points are scored, factors such as:

• How responsive your website is to the different browser types I.e. Google Chrome, Firefox, and Internet Explorer — this includes Mobile phones!

• How easy it is to crawl your website (or if crawling is even allowed …but we’ll come to this later) through the use of “Sitemaps”

* What kind of keywords your website has (i.e. In our examples if the user was to search for a query like “Colours” no domain will be returned — as the search engine has not (yet) crawled a domain that has any keywords to do with “Colours”

There are various online tools — sometimes provided by the search engine providers themselves that will show you just how optimized your domain is. For example, let’s use [Google’s Site Analyser](https://web.dev) to check the rating of [TryHackMe](https://tryhackme.com):

![](https://cdn-images-1.medium.com/max/1000/1\*NRdvYHyq0Bp84kQYWUwlkg.png)

**But…Who or What Regulates these “Crawlers”?**

Aside from the search engines who provide these “Crawlers”, website/web-server owners themselves ultimately stipulate what content “Crawlers” can scrape. Search engines will want to retrieve **everything** from a website — but there are a few cases where we wouldn’t want **all** of the contents of our website to be indexed! Can you think of any…? How about a secret administrator login page? We don’t want **everyone** to be able to find that directory — especially through a google search.

Introducing Robots.txt…

Questions:-

> Q)Use the same [SEO checkup tool](https://web.dev/measure/) and other online alternatives to see how their results compare for [https://tryhackme.com](https://tryhackme.com) and [http://googledorking.cmnatic.co.uk](http://googledorking.cmnatic.co.uk)

> A)Mark as Completed

## Task  4 — Beepboop — Robots.txt

### **Robots.txt**

Similar to “Sitemaps” which we will later discuss, this file is the first thing indexed by “Crawlers” when visiting a website.

**But what is it?**

This file must be served at the root directory — specified by the web server itself. Looking at this file's extension of **.txt**, it's fairly safe to assume that it is a text file.

The text file defines the permissions the “Crawler” has to the website. For example, what type of “Crawler” is allowed (I.e. You only want Google’s “Crawler” to index your site and not MSN’s). Moreover, Robots.txt can specify what files and directories we do or don’t want to be indexed by the “Crawler”.

A very basic markup of a Robots.txt is like the following:

![](https://cdn-images-1.medium.com/max/1000/1\*yPvYbVmJ-KjX1FHYfpef3g.png)

In this case:

1\. Any “Crawler” can index the site

2\. The “Crawler” is allowed to index the entire contents of the site

3\. The “Sitemap” is located at [http://mywebsite.com/sitemap.xml](http://mywebsite.com/sitemap.xml)

![](https://cdn-images-1.medium.com/max/1000/1\*CsE3eDpdm2jBScRpOVwjlQ.png)

In this case:

1\. Any “Crawler” can index the site

2\. The “Crawler” can index every other content that isn’t contained within “/super-secret-directory/”.

Crawlers also know the differences between sub-directories, directories, and files. Such as in the case of the second “Disallow:” (“/not-a-secret/but-this-is/”)

The “Crawler” will index all the contents within “**/not-a-secret/**”, but will not index anything contained within the sub-directory **“/but-this-is/”**.

3\. The “Sitemap” is located at [http://mywebsite.com/sitemap.xml](http://mywebsite.com/sitemap.xml)

What if we Only Wanted Certain “Crawlers” to Index our Site?

We can stipulate so, such as in the picture below:

![](https://cdn-images-1.medium.com/max/1000/1\*4Ek4XPL1PcBvYTZRgFD4fg.png)

In this case:

1\. The “Crawler” “Googlebot” is allowed to index the entire site (“Allow: /”)

2\. The “Crawler” “msnbot” is not allowed to index the site (Disallow: /”)

How about Preventing Files From Being Indexed?

Whilst you can make manual entries for every file extension that you don’t want to be indexed, you will have to provide the directory it is within, as well as the full filename. Imagine if you had a huge site! What a pain…Here’s where we can use a bit of [regexing](https://www.rexegg.com/regex-quickstart.html).

![](https://cdn-images-1.medium.com/max/1000/1\*X2GCmyrUJ7u8KdilMEKnJA.png)

In this case:

1\. Any “Crawler” can index the site

2\. However, the “Crawler” cannot index **any** file that has the extension of **.ini** within any directory/sub-directory using (“$”) of the site.

3\. The “Sitemap” is located at [http://mywebsite.com/sitemap.xml](http://mywebsite.com/sitemap.xml)

Why would you want to hide a **.ini** file for example? Well, files like this contain sensitive configuration details. Can you think of any other file formats that might contain sensitive information?

Questions:-

> Q)Where would “robots.txt” be located on the domain “**ablog.com**”?

> A)ablog.com/robots.txt

> Q)If a website was to have a sitemap, where would that be located?

> A)/sitemap.xml

> Q)How would we only allow “Bingbot” to index the website?

> A)User-agent: Bingbot

> Q)How would we prevent a “Crawler” from indexing the directory “/don't-index-me/”?

> A)Disallow: /dont-index-me/

> Q)What is the extension of a Unix/Linux system configuration file that we might want to hide from “Crawlers”?

> A).conf

## Task  5 — Sitemaps

Comparable to geographical maps in real life, “Sitemaps” are just that — but for websites!

“Sitemaps” are indicative resources that are helpful for crawlers, as they specify the necessary routes to find content on the domain. The below illustration is a good example of the structure of a website, and how it may look on a “Sitemap”:

![](https://cdn-images-1.medium.com/max/1000/1\*hYPRf8J48FIYmMourjyy1Q.png)

The blue rectangles represent the **route** to nested-content, similar to a directory I.e. “Products” for a store. Whereas, the green rounded rectangles represent an actual page. However, this is for illustration purposes only — “Sitemaps” don’t look like this in the real world. They look something much more similar to this:

![](https://cdn-images-1.medium.com/max/1000/1\*RqQVQTojnyihJUNd0Bnqvw.png)

“Sitemaps” are XML formatted.

The presence of “Sitemaps” holds a fair amount of weight in influencing the “optimization” and favorability of a website. As we discussed in the “Search Engine Optimisation” task, these maps make the traversal of content much easier for the crawler!

Questions:-

> Q)What is the typical file structure of a “Sitemap”?

> A)XML

> Q)What real-life example can “Sitemaps” be compared to?

> A)Map

> Q)Name the keyword for the path taken for content on a website

> A)Route

Task — What is Google Dorking?

## Task 6   — What is Google Dorking?

### **Using Google for Advanced Searching**

As we have previously discussed, Google has a lot of websites crawled and indexed. Your average Joe uses Google to look up Cat pictures (I’m more of a Dog person myself…). Whilst Google will have many Cat pictures indexed ready to serve to Joe, this is a rather trivial use of the search engine in comparison to what it can be used for.\


Say if we wanted to narrow down our search query, we can use quotation marks. Google will interpret everything in between these quotation marks as exact and only return the results of the exact phrase provided…Rather useful to filter through the rubbish that we don’t need as we have done so below:

![](https://cdn-images-1.medium.com/max/1000/1\*xTwBiQTacMOmZTUshbx1DQ.png)

### R**efining our Queries**

We can use terms such as “**site**” (such as bbc.co.uk) and a query (such as “gchq news”) to search the specified site for the keyword we have provided to filter out content that may be harder to find otherwise. For example, using the “site” and “query” of “bbc” and “gchq”, we have modified the order in which Google returns the results.

In the screenshot below, searching for “gchq news” returns approximately 1,060,000 results from Google. The website that we want is ranked behind GCHQ’s actual website:

![](https://cdn-images-1.medium.com/max/1000/1\*Zl0U09D-AWh75WOo1c6K3w.png)

But we don’t want that…We wanted “**bbc.co.uk**” first, so let’s refine our search using the “**site**” term. Notice how in the screenshot below, Google returns with much fewer results? Additionally, the page that we didn’t want has disappeared, leaving the site that we did want!

![](https://cdn-images-1.medium.com/max/1000/1\*oka6fGw5fZmg5YLi78DA9w.png)

So What Makes “Google Dorking” so Appealing?

First of all — and the important part — it’s legal! It’s all indexed, publicly available information. However, what you do with this is where the question of legality comes into play…

A few common terms we can search and combine include:

![](https://cdn-images-1.medium.com/max/1000/1\*PMegyJAUp08RSkNb\_7yCYg.png)

For example, let’s say we wanted to use Google to search for all PDFs on bbc.co.uk:

The search query would be — site:bbc.co.uk filetype:pdf

Giving us the following results:-

![](https://cdn-images-1.medium.com/max/1000/1\*AsLi6kJyXCnX34mnJypIJw.png)

Great, now we’ve refined our search for Google to query for all publically accessible PDFs on “**bbc.co.uk**” — You wouldn’t have found files like this “Freedom of Information Request Act” file from a wordlist!

Here we used the extension **PDF**, but can you think of any other file formats of sensitive nature that **may** be publically accessible? (Often unintentionally!!) Again, what you do with any results that you find is where the legality comes into play — this is why “Google Dorking” is so great/dangerous.

Here is a simple directory traversal example:-

![](https://cdn-images-1.medium.com/max/1000/1\*s5Soa0EkVpGRPrWSqBA8Ww.png)

Questions:-

> Q)What would be the format used to query the site bbc.co.uk about flood defenses?

> A)site: bbc.co.uk flood defenses

> Q)What term would you use to search by file type?

> A)filetype:

> Q)What term can we use to look for login pages?

> A)intitle: login

### Conclusion

I do hope that you enjoyed this writeup as much as I did while solving this room!

Thank you for reading this blog and stay tuned as I try to close down more SOC alerts……

## Your opinion matters

My audience has a voice. Feel free to reach out to me on my socials (links are on top of this page), for any queries to be addressed.Dropping a sweet message would make my day

Let your opinion about this write-up be known, by selecting any one of the emojis below!
