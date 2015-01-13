---
layout: post
title: 'How Fastly Builds Support, Part 2'
---

_Note: this is the second part of a multi-part series on how Fastly architects and
builds our support process. You can read part one [here.](http://aspires.github.io/2015/01/05/How-Fastly-Builds-Support-p1/)_

## Part 2: What the customer experiences, and how that happens

What customers encounter when evaluating and onboarding with Fastly isn't arbitrary.
It's an experience that we've intentionally crafted. This post will discuss what
customers experience, and what we have in place to make sure it happens every 
time, for every customer. 

## The customer process

Before we go too deep into our support scaling process, lets take a quick look at
what happens when a person or company signs up for Fastly. Inevitably, this shapes
the support need and the service we provide, so it's important to keep this in
mind.

Most customers come to us with a scaling or ops need. They may be looking
for a new CDN vendor, they may have a difficult problem to solve such as scaling
a service API, or they may just be growing exponentially. In any case,
there's an obvious operational pain point that Fastly can solve.

We intentionally provide a frictionless sign-up process so customers can begin
configuring and testing without needing to talk to a human first. We're ready
to assist, and we make sure that new customers feel free to reach out, but we
don't force ourselves into the picture unnecessarily.

This is a core value of Fastly's support: we give customers as much (or as little)
assistance as they want, exactly when they determine.

Inevitably, customers do reach out with questions during the set-up process. This
is infrastructure &mdash; communication is to be expected and encouraged. Either over
some email or phone exchanges, we discuss fine-tuning
the system for the customer's needs. We're intentionally flexible as a service;
the customer knows their application and needs better than we ever will. But that doesn't
mean that there aren't onboarding questions.

Some customers can configure their service on their own, and move traffic
over quickly and easily. We've put a great deal of work into our documentation
and application design to enable self-service. But, there are always cases where
our teams need to assist. In that case, we may spin up an IRC room for our team
and the customer to coordinate the switch-over, or debug any set-up issues in real time.
Sometimes chatting for 15 minutes can save days of frustrating email exchange.
We'd rather get to the bottom of things right away.

At this point some portion of a customer's traffic has been moved over. There
may be a slow ramp over time. We may be serving a niche portion of a customer's
traffic. We may get the 100% of a customer's public traffic in one day. In any
case, some traffic is now flowing through the customer's network.

In many cases, this is where the interest and support ends. With Fastly, 
it's only the beginning.

Because we're a CDN, we need a connection to our customers' origin servers. This gives us
the ability to see service issues or error spikes almost immediately. Our teams can
proactively reach out in the event of a service disruption. We then work with
the customer as needed to  adjust their CDN or troubleshoot issues.

This ability to proactively assist is possibly the most impressive post of our
support. If you're planning support at your company, I'd like you to have one takeaway from this article:
find a problem your users have that you can predict and proactively
reach out when you see issues arise. A fast response to a customer's ticket is
amazing, but if you can spot a problem before it starts, that's even better.

At some point, a customer may want to put more traffic on to Fastly, fine-tune their
current traffic for a higher hit ratio, build in automated purging, or set up
detailed logging from the edge. This is a more traditional, consultative support.
We view ourselves as scalability partners for our customers, and this is an
extremely rewarding part of the job. We push the limits of what can be offloaded,
and it's fun to work with customers from an architectural standpoint to help hit
their goals.

This has basically been the support process for every single Fastly customer from
day one, with _very_ few exceptions. This experience is what we work on scaling and
improving. We've absolutely made some changes to how we prepare and carry this
process out on our end, but there hasn't been major changes to what we aim for
when providing support. If you were to speak with an early Fastly customer
and a recently ramped Fastly customer, regardless of size, the two customers should describe roughly the same experience. That's not by accident.

## The support process

So what's happening under the hood during what I described above? What steps and processes
do we have in place to make customer set-up and traffic ramping go smoothly?

Pull up a chair, and I'll go right into the thick of things.

Our process starts when the customer contacts Fastly to investigate the product,
or shortly after the customer begins configuring a service after signing up. We then
discuss their end goals over email, phone, IRC, or in person. More often than
not, our [documentation](https://docs.fastly.com/) can help them get set up with most configurations.
But, in the off chance that our documentation doesn't address what they're looking for, we work
directly with the customer over the course of a few days or weeks to build up a
configuration that does what they need.

This configuration is usually done in our web application, but occasionally
we dig in and write some VCL (Varnish Configuration Language, the scripting language
that powers our caching system) to get things done. We may help with setting up
logging and analytics, but those are also easy to self-provision.

Now we're ready to start testing traffic with the customer. To prep for this we
work with our ops and network engineering teams to forecast traffic. As we're now serving a
consistent 1.8 million requests per second worldwide, individual sites and
customers don't cause the network delta they once did, but we still loop in
everyone. When it's time for a customer to finally flip the switch, we have a
group of folks standing by from ops, neteng, product engineering, and support.

Of course, this process doesn't always happen exactly as I describe here. The
process is as unique as their own application, so we help iteratively as needed.
Every few weeks, customers may come back and file a ticket or two, or bump us in
IRC, but the bulk of the work is up-front.

The actual coordination of these processes is jointly run by the customer's 
account manager and our support team. Our account managers will typically get
the relevant information regarding a turn-up, and plan with our support and 
engineering teams for a successful traffic switchover. The main takeaway is that
the entire company contributes to the customer success. It's the majority of what
our support team does on a daily basis, but every team at Fastly is partially
involved with and responsible for customer success.

## Next time

The next post in this series will dive into the structure of Fastly's support
team, and how the team interacts with the rest of the company. This has been the 
most requested topic so far, so I'm excited to publish it. All things equal, this
team and cross-company interaction is possibly the most unique aspect of our
support architecture.  [Follow me on twitter](https://twitter.com/austinspires) 
to hear when updates are live.
