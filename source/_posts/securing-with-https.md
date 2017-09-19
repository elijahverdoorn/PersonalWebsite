---
title: Securing with HTTPS and Let's Encrypt
date: 2017-09-18 22:45:22
tags:
---

# Why?

This project wasn't really necessary, but it feels right, and I support encrypting traffic in general. I want to show that support by practicing what I preach, so I decided that I should go for it and force all traffic to this site to be HTTPS traffic. Additional motivation was the upcoming changes to Chrome in version 62, best summarized by this image:

![Chrome HTTPS chart](chrome.png)

This means that if I were to add an input field to this post, say for comments, and didn't have HTTPS set up, I'd end up with a warning going to viewers using Chrome - not good for traffic or engagement. I was alerted to these changes by Troy Hunt, a security expert who wrote a [great blog post about it](https://www.troyhunt.com/life-is-about-to-get-harder-for-websites-without-https/), and with a few hours to spare today I decided to dive into some configuration files and make this happen.

# How?

I'll start by saying that I'm no expert at this, and I'm not trained as a sysadmin, nor am I as versed in linux networking tools as I'd like to be. I knew about [Let's Encrypt](https://letsencrypt.org/) from some reading I'd done in the past, and heard that they'd give you a certificate for free, so I settled on that. A little more digging led me to [CertBot](https://certbot.eff.org/), which is run by the EFF. Usually I would be skeptical of anything messing with certificates that I didn't make myself, but I decided for the sake of my sanity that I'd trust it, generally having heard good things about the EFF and their work. I followed their installation steps for my server OS, and ran it, specifying my server stack and providing some basic info. Quick restart of the server, and all seemed good, so I went to check it in my browser.

I had no website anymore. Awesome. 404 on my root page, HTTP and HTTPS. To the config files! I use nginx to serve this site, so I took a look at my virtual host configuration. Here's what I found:

```
server {
        listen 80;
        listen [::]:80;

        server_name elijahverdoorn.com;

        root /srv/www/elijahverdoorn.com;
        index index.html;

        location / {
                try_files $uri $uri/ =404;
        }

        location ~ /\.ht {
                deny all;
        }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/elijahverdoorn.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/elijahverdoorn.com/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot


    if ($scheme != "https") {
        return 301 https://$host$request_uri;
    } # managed by Certbot

}
```

Exactly how I wanted it. Certbot was managing the certificate itself, and all the traffic was being routed to HTTPS. Some cursing and a bit of digging later, I discovered that the tutorial I had followed when deploying this site in the first place was not HTTPS friendly, and wasn't going to work. See, that tutorial was aimed at getting something going fast, so it instructed me to edit the default server configuration, which was conflicting with the new virtual host configuration. A quick fix of that, and.... "Too many Redirects". Grrrr...

What happened? I'll spare all the details, but after much digging and restarting of my server, I found that I had a bad CNAME record in the server's web configuration panel. Deleted the record, and BAM! HTTPS enabled!

# What now?

Let's Encrypt certificates are valid for 90 days. Clearly, I don't want to have to manually re-set the certificate myself every three months (honestly, I'd probably just forget and break everything). Luckily, people much smarter than myself have solved this one too, enter the `cron` system. I've used `cron` once before, but I always forget how it works exactly, and in this case I really didn't want to make a mistake. Cron's setup can seem a bit intimidating, here's the line I needed to get the `$ certbot renew` command to run at 2am on the first day of every other month:

```
0 2 1 */2 * certbot renew
```

Luckily, there's a tool for this too - I found [Crontab.guru](https://crontab.guru/) to be really helpful. Now, renewing the certificate is automatic, once every other month.

# That it?

For now, yeah. It really was easy, and I had more problems than the average. I _highly_ encourage everyone to give this a try on their sites, even if the site is more a side project than it is an actual platform. It's a simple, effective, concrete way to support good practices on the web, and learn something new in the process.
