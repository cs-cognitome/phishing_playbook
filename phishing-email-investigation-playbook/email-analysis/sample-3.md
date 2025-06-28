# Sample-3

As for the 3rd one I've chosen The Planet's Prestige — BTLO retired challenge. I'll go through the email and will solve the challenge as well. \
\
Let's start from email artifacts gathering. \


**1) Download .eml file on ParrotOS virtual machine → unzip the file.** \
\
![](<../../.gitbook/assets/image (14).png>)\
\
\
**2) For manual analysis I prefer Sublime Text, but you can use any editor you like** (Pluma, VSCodium, NotePad++ (if on Windows)).&#x20;

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

\
**3) So what useful information we can gather immediately while surfing the .eml file?**&#x20;

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

* Delivered-To:   themajoronearth@gmail.com  — the email address of the person who received the email\

* Received by — 1-st received by from the top is closest to the recipient&#x20;
* The very last (or 1-st from the bottom) received-by field will be the closest to the sender&#x20;

{% tabs %}
{% tab title="What was found here? " %}
1. Email service: emkei.cz&#x20;
2. IP address: 93.99.104.210
{% endtab %}

{% tab title="What we need to do?" %}
1. Check email service&#x20;
2. Check IP reputation&#x20;
3. Check domain reputation (in our case that's domain we can see in the Return-Path: @microapple.com)&#x20;
{% endtab %}
{% endtabs %}

\
Let's start from the email service — in this case simle google check has done the job. We can see that it is fake mail server.&#x20;

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

\
IP address: let's quickly check it in Virus Total.&#x20;

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Though no vendor shows any malicious activity, we'll go to Relations to check overall communication.&#x20;

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

Lot's of emkei.cz connections so far. \
\
Next:&#x20;

*   Authentication-Results: `spf=fail` \
    \
    <mark style="color:red;">**What does it mean?**</mark> Literally the following:  `domain @microapple.com does not permit 93.99.104.210 as sender` \


    <div align="left"><figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure></div>



* Return-Path: [billjobs@microapple.com](mailto:billjobs@microapple.com)\
  \
  <mark style="color:red;">**What's Return-Path first of all?**</mark> It is an email header and it tells SMTP servers where to send non-delivery notifications (bounces). \
  \
  Well, in this case it does match visible "From" address which is also `billjobs@microapple.com`



* To: `themajoronearth@gmail.com`
* Subject: A hope to CoCanDa&#x20;
* From: "Bill" [`billjobs@microapple.com`](mailto:billjobs@microapple.com)&#x20;
* Reply-To: `negeja3921@pashter.com`&#x20;

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

First, what we can see is that `From` and `Reply-To` fields are different. Which is very very suspicious. Because when you reply you want your email to get to the sender, not to some other person/email address.&#x20;



* **Content-Type**: multipart/mixed; boundary=BOUND\_600FB98E0DCEE8.49207210\
  \
  **What does it mean?** \
  \
  This header means the email is composed of multiple parts (such as text and attachments), each separated by the specified boundary string, allowing email clients to correctly parse and display all included content.\
  \
  So, in our case we should expect text + attachment as the content-type is mixed.&#x20;



* **Message-Id**:  [20210126064118.1993E221F8@localhost](mailto:20210126064118.1993E221F8@localhost)\
  \
  In the nutshell: \
  The Message-ID is a critical forensic artifact in email investigation. It helps uniquely identify, trace, and analyze emails, providing clues about their origin, authenticity, and potential manipulation. However, since it can be forged, it should always be analyzed in context with other header fields\
  \
  A Message-ID ending with `@localhost` suggests it was generated on a local server, which could be a sign of a test email, misconfiguration, or, in some cases, a sign of spoofing or malicious activity\
  \
  The Message-ID is designed to be globally unique, so it can be used to track a specific email across different mailboxes, servers, and logs



* **Date**: Tue, 26 Jan 2021 01:41:18 -0500 (EST)\
  \
  While can be spoofed, can be also very useful for crossreferencing. \




Also, we can see that there's some encoded content and we can decode it because we know the type of encoding: base64.&#x20;



* **Content-Transfer-Encoding**: base64 \
  \
  <mark style="color:red;">**What is base64?**</mark> \
  \
  **Short note:**&#x20;

> Base64 encoding is a method that converts binary data into a text string using 64 ASCII characters, making it safe to transmit binary files (like images or attachments) over systems that only support text

We need to decode it to see what's there. That's where CyberChef comes in handy.&#x20;

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

> "Solve the puzzle I sent as an attachment for the next steps."
>
> "...my advice for the puzzle is “Don't Trust Your Eyes”"

&#x20;Okay, solve the puzzle but "don't trust your eyes". Sort of a hint. \




**4) Let's go to the attachment, which we can see as PuzzleToCoCanDa.pdf file**

<div align="left"><figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure></div>

Here we have one more base-64 encoded data, so CyberChef here we go again.&#x20;

1. Decode it.&#x20;
2. Convert it to hex.&#x20;

<mark style="color:red;">**Why convert it to hex?**</mark>&#x20;

50 4b 03 04 — the first bytes of the file make file signature or file header. We always need to take a look at the file signature to find out if the file type is genuine.&#x20;

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

50 4b 03 04 — first bytes in our case — and we can check them here: [https://www.garykessler.net/library/file\_sigs\_GCK\_latest.html](https://www.garykessler.net/library/file_sigs_GCK_latest.html)

{% embed url="https://www.garykessler.net/library/file_sigs_GCK_latest.html" %}

<div align="left"><figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure></div>

So, what can we see from simple checking: apparently our attachment is not a .pdf file but .zip file, which is indeed very interesting. \
\
→ Save it as attachment.zip.

<div align="left"><figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure></div>

→ Unzip it and what we can see is 3 files: an image, .pdf and .xlsx&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure></div>

→ When open .pdf file \
\
**Short note:** \
There are two ways (maybe more, I am exploring it now) in Linux to check if the file has it's genuine file type:&#x20;

{% code overflow="wrap" %}
```bash
1. file yourfile.pdf

#If the file is a genuine PDF, the output will include "PDF document". This command #checks the file's signature (magic number), which for PDFs is %PDF at the beginning #of the file.

2. head -c 4 yourfile.pdf

#The output should be %PDF if the file is truly a PDF.

```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

> Location to send 1 Billion CoCanDs is in Money.xlsx (let's just leave it here)&#x20;



→ Let's open Money.xlsx file. We have a message on the Sheet 1, some kind of StarWars stuff. But..&#x20;

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

But... We have two sheets here. The second one is completely empty or maybe just looks this way. Lets clear the formatting.&#x20;

<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

\
It does look like base64. So we open CyberChef one more time to read what's in the message.&#x20;

> "The Martian Colony, Beside Interplanetary Spaceport."

\
Well, that's supposed to be a location of a "threat actor". \
\
\
What I could not find in the uncovered files was the first/last name of this malicious actor. \


→ Using `exiftool` to find out any additional information in the attachment files. Checked all of them and found a name & surname of Pestero Negeja which correlates with Reply-To username.&#x20;

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

