# Sample-1

Scenario has been taken from BTLO challenge "Phishing": a user has received a phishing email and forwarded it to the SOC. Can you investigate the email and attachment to collect useful artifacts?



**1) Unzip the .eml file with btlo password.**

<div align="left"><figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure></div>

\
**2) Open it via Visual Studio Code (use whatever text editor you prefer/like/have installed).**

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

\
**3) Let's gather all the basic information we can find in the email.**\
\
Delivered-To: johnsmith123@gmail.com\
From: Mail Delivery System Mailer-Daemon@se7-syd.hostedmail.net.au\
Reply-To: --\
Return-Path: --\
To: kinnar1975@yahoo.co.uk\
Subject: Undeliverable: Website contact form submission\
Date: Fri, 19 Mar 2021 16:49:19 +0000\
**X-Originating-IP**: 103\[.]9\[.]171\[.]10\
\
Then we can see a message that it was not delivered to this mail address:

<div align="left"><figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure></div>



**4) Let's check up this IP address in VirusTotal:**\
\
Nothing was found so far, but we also need to check Relations field to have a bigger picture.

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

Though it has some suspicious communicating files.

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

And lots and lots of hostnames pointed to that IP address.

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>



**5) Let's perform the reverse DNS on this IP address via** [**https://whois.domaintools.com/103.9.171.10**](https://whois.domaintools.com/103.9.171.10)

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

The resolve host is: the hostname tied to an IP address by reverse DNS lookup.

```
c5s2-1e-syd.hosting-services.net.au 
```

It tells us about location, hosting services and cluster notation e.g. c5s2-1e (cluster 5, shelf 2, node 1e, allows you to group neighboring IPs, usually for group blocking).\
\
Country: Australia.\
City: Sydney.





**6) One more interesting email header — `X-MS-Has-Attach: yes`**

<div align="left"><figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure></div>

That is Microsoft own flag that simply says: "this message contains at least one attachment".\
\
To see the name of attachment — I downloaded Thunderbird to open the .eml file in it:&#x20;

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Name of attachment: Website contact form submission.eml

Size: 3.9 kB



**7) There's a URL has been also found in the attachment:**

hxxps\[://]35000usdperwwekpodf\[.]blogspot\[.]sgp=9swghxxps\[://]35000usdperwwekpodf\[.]blogspot\[.]co\[.]il?o=0hnd

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Used CyberChef to defang it.

Why do we need to defang IPs or URLs? Defanging prevents accidental clicks and execution during analysis or reporting. It is a safety layer between the analyst and the threat.





**8) What service is this webpage hosted on? Let's check the URL with** [**urlscan.io**](https://urlscan.io) **first.**

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

From the captures we can see that it is blogspot.com. After quick search in google we have an additional confirmation that hosted webpage is blogspot.com (blogger.com).

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>



**9) What's the heading text on the page? You can use either** [**https://urlscan.io**](https://urlscan.io) **or** [**https://www.url2png.com/**](https://www.url2png.com/)

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

Heading text: Blog has been removed.
