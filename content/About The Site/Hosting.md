+++
title = "Hosting"
description = "TL;DR: Netlify"
date = 2019-04-21
+++

{{% alert theme="info" %}} Previously the site was hosted across a number of providers to maximize the respective benefits of each of their free tiers. Now, however, Netlify combines many of their best aspects into one service.{{% /alert %}}

~~The site's CDN is handled by [Cloudflare](https://www.cloudflare.com/). Free CDN, DNS, optimizations, and added security.~~

~~Images are hosted using [Backblaze B2](https://www.backblaze.com/b2/cloud-storage.html). Although it doesn't support many of the features of other cloud storage solutions, it's a good bit cheaper. More importantly, it allows for the creation of simple request and bandwidth caps that AWS and Google don't support. I don't want a small personal site to scale up in case of an attack; I want it to stop loading large assets to minimize the damage. Or worse, someone trying to embed my content elsewhere. Even if B2 can't easily set bucket policies to only route through Cloudflare, the caps are an absolute protection against overcharging.~~

~~The site itself is hosted on [Amazon S3](https://aws.amazon.com/s3/). Unlike Backblaze, AWS doesn't have a simple way to automatically shut down a site in case of an attack. That being the case, I really have no choice but to only host small files there; the only limit protecting me there is the request limit. As long as the files are kept small, that should saturate before paying for bandwidth becomes a massive issue.~~

#### Edit 19 April 2019:

Transferred everything over to Netlify. Previously I had avoided that option because I want to avoid being locked into an ecosystem as much as possible, and because I wasn't sure if Netlify's model was sustainable.

In practice though, these fears seem poorly founded. The ecosystem, while it does exist, is far from a walled garden; it's perfectly possible to use Netlify purely as a static host and spread out other features across different providers. 

And even if it weren't possible, I found myself asking why I would even want to. I used B2 because of its free 10GB of storage and 1GB/day bandwidth. Netlify offers a free 100GB storage and 100GB egress per month. Ditto for hosting advantages compared to Firebase. Direct integration with Github is super convenient. In a pure CDN role Netlify probably isn't as good as Cloudflare, but it has the latency advantage of being both the host and CDN, and since Netlify doesn't even have my payment information I don't even *need* a CDN to protect the site against DOS attacks. And to top it off there's nothing stopping me from using both if I wanted to. 

Other miscellaneous stuff:

>>   * Netlify's forms look like a useful feature I'd like to use sometime, even if the monthly limit of 100 is a bit low.  
>>   * 125k free serverless functions is significantly lower than other cloud services providers, but there's nothing preventing me from using their tools in tandem with Netlify. The same thing goes for many features that Netlify doesn't have (yet).  
>>   * Technically the easiest (and most powerful) solution would probably be to plop a CDN in front of [Google Cloud's always free virtual server](https://cloud.google.com/free/), but that would defeat the point of having a static website. Perhaps I'll crack at some point in the future. 