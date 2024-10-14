# Overview
+ Amazon CloudFront is a web service that **speeds up distribution of your static and dynamic web content**, such as .html, .css, .js, and image files, to your users.
+ CloudFront delivers your content through a worldwide network of data centers called **edge locations**.
+ When a user requests content that you're serving with CloudFront, the request is **routed to the edge location that provides the lowest latency (time delay)**, so that content is delivered with the best possible performance.
# CloudFront use cases
+ CloudFront can **speed up the delivery of your static content** (for example, images, style sheets, JavaScript, and so on) to viewers across the globe
+ CloudFront offers several options for **streaming your media to global viewers**—both pre-recorded files and live events.
+ **Encrypt specific fields** throughout system processing
+ Customize at the edge: Using Lambda@Edge with CloudFront enables a variety of ways to **customize the content that CloudFront delivers**.
+ **Serve private content** by using Lambda@Edge customizations
# **Regional edge caches**
+ CloudFront points of presence (POPs) (**edge locations**) make sure that popular content can be served quickly to your viewers.
+ CloudFront also has **regional edge caches** that bring more of your content closer to your viewers, even when the content is not popular enough to stay at a POP, to help improve performance for that content.
+ Regional edge caches are located **between your origin server and the POPs**—global edge locations
+ Regional edge caches have a **larger cache** than an individual POP
# Distributions
+ When you want to use CloudFront to distribute your content, you create a distribution and choose the configuration settings you want
+ You can use **distributions** to serve the following content over HTTP or HTTPS: 
    + Static and dynamic download content, for example, .html, .css, .js, and image files, using HTTP or HTTPS.
    + Video on demand in different formats, such as Apple HTTP Live Streaming (HLS) and Microsoft Smooth Streaming
    + A live event, such as a meeting, conference, or concert, in real time
+ When you create or update a distribution, you provide information about one or more locations—known as **origins**—where you store the original versions of your web content. 
+ Each origin is either an Amazon S3 bucket or an HTTP server
+ A **cache behavior** lets you configure a variety of CloudFront functionality for a given URL path pattern for files on your website.
+ Allowed HTTP Methods 
    + **GET, HEAD:** You can use CloudFront only to get objects from your origin or to get object headers.
    + **GET, HEAD, OPTIONS:** You can use CloudFront only to get objects from your origin, get object headers, or retrieve a list of the options that your origin server supports.
    + **GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE:** 
+ In CloudFront, an alternate domain name, also known as a **CNAME,** lets you **use your own domain name** (for example, www.example.com) in your files’ URLs instead of using the domain name that CloudFront assigns to your distribution.
+ Amazon CloudFront **supports using WebSocket**, a TCP-based protocol that is useful when you need long-lived bidirectional connections between clients and servers.
# Policies
+ With CloudFront *policies*, you can control the values that are included in the **cache key** for objects that are cached at CloudFront edge locations.
+ When there’s a *cache miss* (the requested object is not cached at the edge location), CloudFront sends a request to the origin to retrieve the object. This is called an **origin request**. 
+ You control the cache key with a **cache policy** and the origin request with an **origin request policy**.
+ You can use a cache policy to improve your cache hit ratio by controlling the values (**URL query strings, HTTP headers, and cookies**) that are included in the cache key
+ By default, the cache key for a CloudFront distribution includes the following information: 
    + The domain name of the CloudFront distribution (for example, d111111abcdef8.cloudfront.net)
    + The URL path of the requested object (for example, `/content/stories/example-story.html`)
    + All URL query strings, HTTP headers, and cookies that you include in the cache key (using a cache policy) are **automatically included in origin requests**
+ Use the origin request policy to specify the information that you want to include in origin requests, but **not include in the cache key**.
+ You can also use an origin request policy to **add additional HTTP headers** to an origin request that were not included in the viewer request. 
# Manage Contents
+ When you want CloudFront to distribute content (objects), you **add files to one of the origins** that you specified for the distribution, and you expose a CloudFront link to the files.
+ There are two ways to **update existing content** that CloudFront is set up to distribute for you: 
    + Update files by **using the same name**
    + Update by **using a version identifier in the file name**
    + We recommend that you use a version identifier in file names or in folder names, to help give you more control over managing the content that CloudFront serves.
+ You can **remove files from your origin** that you no longer want to be included in your CloudFront distribution. However, CloudFront will continue to show viewers content from the edge cache until the files expire.If you want to remove a file right away, you must do one of the following: 
    + **Invalidate the file.**
    + **Use file versioning.** 
+ If you have content that you want to restrict access to, you can create **signed URLs**. For example, if you want to distribute your content only to users who have authenticated, you can create URLs that are valid only for a **specified time period or that are available only from a specified IP address**.
+ You can configure CloudFront to return a custom error response to the viewer instead of the one returned by origin
+ CloudFront provides several options for **securing content** that it delivers. The following are some ways you can use CloudFront to secure and restrict access to content: 
    + Configure **HTTPS** connections
    + Prevent users in specific **geographic locations** from accessing content
    + Require users to access content using CloudFront **signed URLs or signed cookies**
    + Set up **field-level encryption** for specific content fields
    + Use **AWS WAF** to control access to your content
+ serving private content 
    + You can configure CloudFront to require that users access your files using either *signed URLs* or *signed cookies*. 
+ Use signed URLs in the following cases: 
    + You want to restrict access to individual files, for example, an installation download for your application.
    + Your users are using a client (for example, a custom HTTP client) that doesn't support cookies.
+ Use signed cookies in the following cases: 
    + You want to provide access to multiple restricted files, for example, all of the files for a video in HLS format or all of the files in the subscribers' area of website.
    + You don't want to change your current URLs.
+ You can optionally secure the content in your Amazon S3 bucket so that users can access it through CloudFront but cannot access it directly by using Amazon S3 URLs.
+ If you use a custom origin, you can optionally set up custom headers to restrict access. 
# Optimizing caching and availability
## **Improving the cache hit ratio**
+ You can improve performance by increasing the proportion of your viewer requests that are served directly from the CloudFront cache instead of going to your origin servers for content. This is known as **improving the cache hit ratio**.
+ To increase your cache hit ratio, you can configure your origin to **add a [Cache-Control max-age](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)** directive to your objects, and specify the longest practical value for `max-age`. 
+ **CloudFront Origin Shield** can help improve the cache hit ratio of your CloudFront distribution, because it provides an additional layer of caching in front of your origin.
+ If you configure CloudFront to **cache based on query string parameters**, you can improve caching if you do the following: 
    + Configure CloudFront to forward only the query string parameters for which your origin will return unique objects.
    + Use the same case (uppercase or lowercase) for all instances of the same parameter.
    + List parameters in the same order. 
+ If you configure CloudFront to **cache based on cookie values**, you can improve caching if you do the following: 
    + Configure CloudFront to **forward only specified cookies** instead of forwarding all cookies.
    + Create **separate cache behaviors for static and dynamic content**, and configure CloudFront to forward cookies to your origin only for dynamic content.
    + If possible, create separate cache behaviors for dynamic content when cookie values are unique for each user (such as a user ID), and dynamic content that varies based on a smaller number of unique values.
+ If you configure CloudFront to cache **based on request headers**, you can improve caching if you do the following: 
    + Configure CloudFront to forward and cache based on **only specified headers** instead of forwarding and caching based on all headers. 
    + Try to avoid caching based on request headers that have large numbers of unique values.
    + Remove Accept-Encoding header when compression is not needed
    + Serving media content by using HTTP
## Optimizing high availability with CloudFront origin failover
+ To set up origin failover, you must have a distribution with at least two origins. Next, you create an origin group for your distribution that includes two origins, setting one as the primary. Finally, you create or update a cache behavior to use the origin group.
+ CloudFront **routes all incoming requests to the primary origin**, even when a previous request failed over to the secondary origin. CloudFront only sends requests to the secondary origin after a request to the primary origin fails.
+ CloudFront fails over to the secondary origin only when the HTTP method of the viewer request is **`GET`, `HEAD`, or `OPTIONS`**.
+ By default, CloudFront tries to connect to the primary origin in an origin group for as long as 30 seconds (3 connection attempts of 10 seconds each) before failing over to the secondary origin.
+ To fail over more quickly, specify a shorter connection timeout, fewer connection attempts, or both.
## Managing cache expiration
+ You can **control how long** your files stay in a CloudFront cache before CloudFront forwards another request to your origin.
+ **Reducing** the duration allows you to serve **dynamic **content.
+ **Increasing** the duration means that your users get **better performance** because your files are more likely to be served directly from the edge cache.
+ A longer duration also **reduces the load on your origin**.
+ Typically, CloudFront serves a file from an edge location until the cache duration that you specified passes—that is, until the file expires.
+ If a file in an edge location **isn't frequently** requested, CloudFront might evict the file—**remove the file before its expiration date**
+ By default, each file automatically **expires after 24 hours**, but you can change the default behavior in two ways: 
    + To change the cache duration for all files that match the same path pattern, you can change the CloudFront settings for **Minimum TTL**, **Maximum TTL**, and **Default TTL** for a cache behavior.
    + To change the cache duration for an individual file, you can configure your origin to add a `Cache-Control max-age` or `Cache-Control s-maxage` directive, or an `Expires` header field to the file.
# Customizing at the edge with functions
+ With Amazon CloudFront, you can write your own code to customize how your CloudFront distributions process HTTP requests and responses.
+ The code runs close to your viewers (users) to minimize latency, and you don’t have to manage servers or other infrastructure.
+ CloudFront provides two ways to write and manage edge functions: 
+ **CloudFront Functions**
    + With CloudFront Functions, you can write lightweight functions in JavaScript for high-scale, latency-sensitive CDN customizations.
    + The CloudFront Functions runtime environment offers **submillisecond startup times**, **scales immediately** to handle millions of requests per second, and is **highly secure**.
    + CloudFront Functions is a **native feature** of CloudFront, which means you can build, test, and deploy your code entirely within CloudFront.
+ **Lambda@Edge**
    + Lambda@Edge is an **extension of [AWS Lambda](http://aws.amazon.com/lambda/)** that offers powerful and flexible computing for complex functions and full application logic closer to your viewers, and is highly secure.
    + Lambda@Edge functions run in a **Node.js or Python** runtime environment. 
    + You publish them to **a single AWS Region**, but when you associate the function with a CloudFront distribution, Lambda@Edge automatically replicates your code around the world.
## ​​​​​​​​​​​​​​​​​​​​​​​​​​​​CloudFront Functions
+ CloudFront Functions is ideal for lightweight, short-running functions for use cases like the following: 
    + Cache key normalization
    + Header manipulation 
    + URL redirects or rewrites 
    + Request authorization
+ ​​​​​​​​​You can invoke CloudFront functions when the following events occur: 
    + When CloudFront receives a request from a viewer (viewer request)
    + Before CloudFront returns the response to the viewer (viewer response)
## Lambda@Edge
+ You can execute Lambda functions when the following CloudFront events occur: 
+ When CloudFront receives a request from a viewer (viewer request)
+ Before CloudFront forwards a request to the origin (origin request)
+ When CloudFront receives a response from the origin (origin response)
+ Before CloudFront returns the response to the viewer (viewer response)
+ There are many uses for Lambda@Edge processing. For example: 
    + A Lambda function can inspect cookies and rewrite URLs so that users see different versions of a site for A/B testing.
    + CloudFront can return different objects to viewers based on the device they're using by checking the `User-Agent` header, which includes information about the devices.
    + Or you could check cookies for other criteria. 
    + A Lambda function can generate HTTP responses when CloudFront viewer request or origin request events occur.
    + A function can inspect headers or authorization tokens, and insert a header to control access to your content before CloudFront forwards the request to your origin.
    + A Lambda function can also make network calls to external resources to confirm user credentials, or fetch additional content to customize a response.
+ To use Lambda@Edge, you write the code for your Lambda function, then set up AWS Lambda to **run the function based on specific CloudFront events (triggers).**
# Reference
[Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)

