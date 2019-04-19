+++
title = "Hosting"
description = "Sure, I could put the whole thing on AWS, but that wouldn't be very safe (or cheap). And yes, Netlify exists, but that comes with limitations of its own. To maximize expandability and control while keeping running costs near zero, I've spread out the hosting over a couple of providers."
date = 2018-09-19
+++

The site's CDN is handled by [Cloudflare](https://www.cloudflare.com/). Free CDN, DNS, optimizations, and added security. 

Images are hosted using [Backblaze B2](https://www.backblaze.com/b2/cloud-storage.html). Although it doesn't support many of the features of other cloud storage solutions, it's a good bit cheaper. More importantly, it allows for the creation of simple request and bandwidth caps that AWS and Google don't support. I don't want a small personal site to scale up in case of an attack; I want it to stop loading large assets to minimize the damage. Or worse, someone trying to embed my content elsewhere. Even if B2 can't easily set bucket policies to only route through Cloudflare, the caps are an absolute protection against overcharging. 

The site itself is hosted on [Amazon S3](https://aws.amazon.com/s3/). Unlike Backblaze, AWS doesn't have a simple way to automatically shut down a site in case of an attack. That being the case, I really have no choice but to only host small files there; the only limit protecting me there is the request limit. As long as the files are kept small, that should saturate before paying for bandwidth becomes a massive issue. 

