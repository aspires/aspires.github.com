---
layout: blog_post
title: 'Level Up Your Log: Pro Tips for Fastly Streaming Logs'
---

**Note:** This is a cross post from [Fastly's blog](http://www.fastly.com/blog/tips-for-streaming-logs/), 
which was ultimately picked up by O'Reilly's Web Ops and Perfomance newsletter

Streaming logs is one of our most popular features. It's fast and flexible, giving operations teams more 
data from the edge than ever before and in real time.

### Create Redundancy With Multiple Feeds
Setting up multiple log feeds for redundancy is so easy that it's often overlooked. Fastly doesn't limit 
the number of log feeds that you can create, and a parallel feed can be created in a matter of seconds.

This enables a new degree of flexibility in logging. Logging from your CDN is now something that can be
approached with the same level of planning as any other tool in your stack. Based on what we've seen, the 
configuration is the easiest way to get started with a comprehensive strategy that accounts for redundancy 
and fast decision-making:

1. Create a log stream pointing to your existing monitoring tools. This may be a syslog server you maintain 
or a service in a supported logging platform such as Splunk, Papertrail, Logentries, and Loggly.
2. Create a parallel log feed pointing at an Amazon S3 bucket. Our standard S3 configuration defaults to 
sending logs in batches every hour, but this time interval can be adjusted. This should serve as a backup, 
or "cold storage," of your data. On a side note, <a href="https://aws.amazon.com/about-aws/whats-new/2014/01/21/announcing-new-amazon-ec2-m3-instance-sizes-and-lower-prices-for-amazon-s3-and-amazon-ebs" target=_blank">Amazon recently reduced their S3 prices</a>.
3. Add a "quick view" service if you need a separate solution from your standard tools. 
Third party services like <a href="https://www.splunkstorm.com/" target="_blank">Splunk</a> 
or <a href="https://papertrailapp.com/dashboard" target="_blank">Papertrail</a> are great for this. 
They provide a way for your entire team to quickly access your logs from any location, and this option 
won't disrupt your main monitoring tools or your backup logs.

### Log Only What You Need
We don't <i>really</i> need any more firehoses in our lives. Data from the edge is now a solved problem thanks 
to the above configurations, so the biggest issue is figuring out how to actually extract meaningful information 
from that data.

If you're already using Fastly, you're probably familiar with our 
<a href="http://docs.fastly.com/guides/21835572/23472072" target="_blank">conditionals in configurations</a>: 
"if statements" based on HTTP header URL content that allow you to fine-tune your CDN configurations so that 
they only affect certain segments of your traffic.

Streaming log configs can also take these conditionals, which allow you to create incredibly specific log 
streams, giving you the exact data that you need.

With these logging configurations, you can configure your service to stream only the log data that matches 
the conditional. There's no need to sift through a pile of irrelevant data in your logging tools if you can 
stop noise from getting into the system.

Some awesome use cases we've already seen include:

* Setting up a user data feed for your marketing group to log only 200s, where the referer, user agent, and 
granular GeoIP information are included.
	* Format string: %h %l %u %t %r %>s req.http.referer req.http.User-Agent geoip.city
	* Conditional: resp.status == 200

* A feed just for 5XX errors with additional data used for diagnosing the request, such as the Fastly POP in use, 
client IP address, regional GeoIP information, and whether the request was over SSL.

	* Format string: %h %l %u %t %r %>s server.datacenter req.http.Fastly-Client-IP geoip.region req.http.Fastly-SSL
	* Conditional: resp.status > 499

* A 404 feed that logs referrer information to see if there are chronic broken links on your page or pointing to your site.
	* Format string: %h %l %u %t %r %>s req.http.referer
	* Conditional: resp.status == 404

* Temporary log feeds used for tracking down elusive edge case bugs. If you know a certain URL path is occasionally erroring, you can set up a feed to log only if the request URL matches an expression and if the request status is equal to 503. You can then add diagnostic-specific information to the logs that would help you track down the root cause.
	* Format string: %h %l %u %t %r %>s resp.http.My-Debug-Header geoip.country_name
	* Conditional: resp.status > 499 && req.url ~ /path/to/debug

###Logging Through the Fastly API
You can even spin up logs services with our API. The following cURL command will stage a service to log 
all responses to a syslog server, and include the referrer header:

=======
<script src="https://gist.github.com/aspires/847806e683b2f4f163e0.js"></script>


Obviously, that cURL command is a nightmare, so we recommend using an <a href="http://docs.fastly.com/api/clients" 
target="_blank">API client</a> instead to save your sanity and soul.

If you already have a rapid, tool-driven operations workflow, you can build in automated creation and deletion of 
logs to quickly gather data as the need arises.

### Make Your Data Work For You
Customers were excited when we first released our streaming logs feature, and then we took it even further when we 
later <a href="/blog/new-fastly-logging-features" target="blank">included support</a> for additional 
logging-as-a-service platforms usage. We're just getting started, and customers are only just scratching the surface 
of what can be done. We're redefining what it means to have a CDN in your stack, and that extends to your logging 
as well.

It's time to put that edge data to work for you rather than spending your time sifting through yet another haystack looking for a needle. You can start setting up these configurations immediately in your <a href="https://app.fastly.com/#configure" target="_blank">app account</a>.

If you don’t have an account yet, you can start testing with a developer account by <a href="/signup/" target="_blank">signing up</a>.
