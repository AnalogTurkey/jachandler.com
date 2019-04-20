+++
title = "Amazon S3 Request Security"
description = "AWS's request rules and lack of useful customizable limits allow attackers to rack up high bills for S3 bucket owners, even on private and empty buckets. The only effective defense is to immediately delete the affected resources when they are targeted. A simple lambda function and settings changes can help mitigate some of the danger."
date = 2018-11-22
+++

{{% alert theme="info" %}} AWS's request rules and lack of useful customizable limits allow attackers to rack up high bills for S3 bucket owners, including on fully private buckets. The only effective defense is to immediately delete the affected resources when they are targeted.{{% /alert %}}

## The Problem

One of my goals with this site was to create the most functional website possible at the lowest possible cost. And sure, setting up a static site hosting bucket on S3 and forgetting about it seems like a simple solution. Just one slight problem – what happens to those costs if traffic (legitimate or not) suddenly spikes? How can I prevent a scenario where a site normally costing a couple cents per month suddenly racks up a bill in the thousands of dollars?

Backblaze B2 has a ready answer to this problem: let the user set request/bandwidth limits and pause the service when those caps are reached. Unfortunately, AWS doesn't have anything like this[^1]. Officially, the recommendation is to use billing alerts to send a notification when projected spending reaches a threshold, but even assuming the overutilized resources can be shut down immediately following the notification, billing is only updated a few times per day, leaving relatively large spans of time vulnerable. 

## What about bucket permissions?

Setting a bucket private or using a bucket policy to only allow trusted connections only prevent public *access* to a file; [anonymous *requests* that end in a 403 error are still possible and are still billed to the bucket owner](http://forums.aws.amazon.com/thread.jspa?messageID=58436). That's been Amazon's policy since the beginning, even though they don't warn users about this.

{{< figure src="S3Request/403charges" type="jpg" width="55%">}}

Even if setting a bucket to "requester pays" is an option for the use case in question, that still doesn't help; [AWS makes a special billing exception for code 403](https://docs.aws.amazon.com/AmazonS3/latest/dev/RequesterPaysBuckets.html#ChargeDetails). 

## What can be done?

The only surefire defense is to delete the bucket, and the best way to get that to happen automatically is through AWS Lambda. The code to do so is straightforward:


```
import boto3
s3=boto3.resource('s3')

def lambda_handler(event, context):

    s3.Bucket('bucketName').objects.all().delete()
    s3.Bucket('bucketName').delete()
```

The two lines of deletion are required because S3 only allows empty buckets to be deleted. Simply emptying the bucket isn't enough; attempts to access empty buckets *still* generate list requests.

Amazon recommends that this sort of script be triggered by a billing alarm. Since billing alarms only update a few times per day (at least once per day, officially), this isn't a very good option for limiting costs: given that S3 automatically scales to handle thousands of requests per second, even an empty bucket can potentially cost more than a dollar per minute when targetted. Letting this run for a few hours pushes this into the hundreds of dollars – all this for a single empty bucket! 

A better way is to use a Cloudwatch alarm triggered by the bucket request metrics. This isn't strictly ideal; after all, there is a limit to how many of these paid metrics you can set up while staying within the free tier. For just a few buckets, though, it shouldn't cost anything extra. 

Under bucket management, enable request metrics. Then in Cloudwatch, create an alarm with the desired metric as a source and set the threshold and time period that you want to trigger the bucket deletion (I used AllRequests >= 5,000 for 1 datapoints within 1 hour – Sum). For the action, have it send a notification to an SNS topic when in alarm state. In Lambda, create a Python function, paste the code, and set the SNS topic as the trigger. 

With that, the buckets will delete themselves when the number of requests directly to a bucket in a short period of time get out of hand. It's not at all an elegant solution, but as far as I'm aware it's the only one that works. With a CDN in front, normal usage won't even touch the bucket most of the time, meaning there is minimal danger of a false alarm. Until there is a better and safer way though, I'm keeping my S3 usage to a minimum.

[^1]:Google Cloud doesn't either. However, they do have a good indefinite free tier which respects its own quotas, which is ideal for small projects. I hear Azure has spending limits, though I haven't used it so I can't comment on how well they work.

