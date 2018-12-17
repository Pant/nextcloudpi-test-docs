---
title: How to configure Let's Encrypt with closed ports 80 and 443
keywords: configuration security letsencrypt network guide
tags: [configuration, security, letsencrypt, network, guide]
#summary: ""
sidebar: en_sidebar
sidebar_folder: 'Configuration'
language: 'en'
permalink: en_How-to-configure-Lets-Encrypt-with-closed-ports-80-and-443.html
folder: en
---

> This entry was originally written by @albrechtar [in this github question](https://github.com/nextcloud/nextcloudpi/issues/186#issuecomment-328333387)

## How to get SSL certs without using Cert Bot (in case you would need to use alternate ports on your instance of NextCloudPi)

You would need to then manually update your SSL certs on your instance of NextCloudPi.

1.  You will need a domain name that allows you to point to other name servers as well as edit the DNS records.  I purchased my own (most free 3rd tier domains would not allow this.  So I recommend you go to namecheap.com and purchase your domain name (they have them for as low as 2.09 for the first year. Then proceed to dynu.com.  Signup and then click the little gear in the top right area it will take you to your control panel [ScreenShot1](#screenshot1).  You will also need to go to namecheap or wherever you get your domain name and add the name servers for Dynu.  They have very easy to follow tutorials and instructions if you are unable to figure this out.

     1.  Click DDNS services.
     2.  Click Add
     3. If you have your own domain use it on the right [ScreenShot2](#screenshot2)
     4.  Enter your public ip address (I used X to block mine you would enter your full ip address), and click save.
     5.  Just to the right you will see a cup with pencils in it that says DNS records you will want to click this. (ScreeenShot3, [ScreenShot4](#screenshot4).

2.  Open another tab in your browser and goto zerossl.com [ScreenShot5](#screenshot5)
     1.  On the left side please click Certificates and Tools [ScreenShot6](#screenshot6).
     2.  Click Start under free SSL Certificate wizard and you will see [ScreenShot7](#screenshot7).
     3.  Enter your email address, enter your domain name (yourdomain.com) select DNS Verification and accept the TOS and SA, and click Next [ScreenShot8](#screenshot8)
     4.  You will be asked to include a www. prefix please select yes.
     5.  You will see that the system generated the CSR [ScreenShot9](#screenshot9).
     6.  Click next and the system will generate the key.[ScreenShot10](#screenshot10).
     7.  You will click the download icon and download both the CSR and the KEY [ScreenShot11](#screenshot11).
     8.  Click next and you will see [ScreenShot12](#screenshot12).
     9.  Now you will need to go back to your Dynu page (remember we left it open and continue to step 3.

3.  Once you are back on your Dynu page you will notice 4 items (node name, type, TTL, and hostname [ScreenShot13](#screenshot13).  Please follow the below steps:
     1.  Change type to be TXT -Text
     2.  Node Name copy and paste your domain TXT Record from your zerossl page.
     3.  Copy and paste the value field from zerossl into the text field on your dynu page [ScreenShot13](#screenshot13). (TTL can stay at 90).
     4.  Repeat step 3c for the other entry (you have two one for www. and one that is just your domain).
     5. SSH into your pi, and type nslookup -q=TXT XXX", where XXX is one of the records you just pasted into the Node name in step 3b.
     6. It will only take a minute or two and then when you run that nslookup it will show you that it sees it (I dont recall the exact wording but it was obvious).
     7. Go back to your openssl and click next. Once it verifies it will issue your account key and your domain crt files.

Once you have these files you have your SSL certificate and you will need to put it in the correct folder on your instance of NextCloudPi.  I am not 100% certain what file to place these into so I will ask @nachoparker to explain that.

I hope this helps, if anyone has any questions please feel free to message here and I will do my best to help. need to then manually update your SSL certs on your instance of NextCloudPi.

By default they live under `/etc/ssl`

```
...
SSLCertificateFile    /etc/ssl/certs/ssl-cert-snakeoil.pem                                                       
SSLCertificateKeyFile /etc/ssl/private/ssl-cert-snakeoil.key
...
```

## Screenshots
<a name="screenshot1"></a> ScreenShot1: ![](https://user-images.githubusercontent.com/19283265/30248880-0bae800a-965a-11e7-8843-fec87e1401a8.png)
<a name="screenshot2"></a> ScreenShot2: ![](https://user-images.githubusercontent.com/19283265/30248881-0f6e18ae-965a-11e7-8eda-dcc740c99af3.png)
<a name="screenshot3"></a> ScreenShot3: ![](https://user-images.githubusercontent.com/19283265/30248882-0fab0124-965a-11e7-9113-884532167867.png)
<a name="screenshot4"></a> ScreenShot4: ![](https://user-images.githubusercontent.com/19283265/30248883-0fb3716a-965a-11e7-858f-4a6c53c261f4.png)
<a name="screenshot5"></a> ScreenShot5: ![](https://user-images.githubusercontent.com/19283265/30248885-0fb899a6-965a-11e7-927f-1a52b0930bbd.png)
<a name="screenshot6"></a> ScreenShot6: ![](https://user-images.githubusercontent.com/19283265/30248884-0fb8388a-965a-11e7-9764-c7c19ed00d68.png)
<a name="screenshot7"></a> ScreenShot7: ![](https://user-images.githubusercontent.com/19283265/30248886-0fb8cb56-965a-11e7-86df-96cd61bb4abd.png)
<a name="screenshot8"></a> ScreenShot8: ![](https://user-images.githubusercontent.com/19283265/30248887-0fb98d70-965a-11e7-8753-aa788fd78541.png)
<a name="screenshot9"></a> ScreenShot9: ![](https://user-images.githubusercontent.com/19283265/30248888-0fe3dd64-965a-11e7-8999-87b663137fac.png)
<a name="screenshot10"></a> ScreenShot10: ![](https://user-images.githubusercontent.com/19283265/30248889-0fe47e72-965a-11e7-933d-e025148611c2.png)
<a name="screenshot11"></a> ScreenShot11: ![](https://user-images.githubusercontent.com/19283265/30248890-0fea86a0-965a-11e7-9083-39914a54d327.png)
<a name="screenshot12"></a> ScreenShot12: ![](https://user-images.githubusercontent.com/19283265/30248891-0feabc42-965a-11e7-9277-3fff58786c10.png)
