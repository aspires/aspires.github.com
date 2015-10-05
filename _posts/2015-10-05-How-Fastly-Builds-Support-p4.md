---
layout: post
title: "How Fastly Builds Support, Part 4"
---

_This is the final part of a multi-part series on how Fastly architects and
builds our support process. You can read [part one](http://aspires.github.io/2015/01/05/How-Fastly-Builds-Support-p1/), [part two](http://aspires.github.io/2015/01/12/How-Fastly-Builds-Support-p2/), and [part three](http://austin.dangerspires.com/2015/02/09/how-fastly-builds-support-p3/) to get prior context._

This article dives into our support team's training processes and explains how our lessons learned can help your support team grow.

### Training

Many customers come to Fastly’s support seeking advice on Varnish, an open source software that’s at the core of our CDN services. Because of this, our team has to be experts on all things Varnish. We also have an incredibly technical product and customer base, so we have to be equally knowledgeable. Even for team members with prior CDN or Varnish experience, Fastly’s technology requires training and continuing education on a regular basis to maintain meaningful support interactions. If you're running a support team, large or small, proper new hire training and continuing education are essential to keeping your quality and team morale up.

Because of this, Fastly needed to embrace having a comprehensive training and onboarding process for our new and existing support team members in the early days. Our current training programs are not formally completed (yet), but we have everything from advanced technical talks with our subject matter experts to informal computer science classes covering the absolute basics to side-by-side pairing sessions. Fastly has reached the point where nearly any new hire can be brought up to full productivity within a few weeks.

The training I mentioned above focuses on just the technical aspects of the job, not the softer skills that make up support interactions. We have training processes for that, too. Support is a skill, and it takes practice. From spotting related problems from specific wording in a ticket to being able to effectively convey appropriate emotions in writing, language skills are crucial for support.

### Timing and tone

With proper technical and tone training in mind, we’ve discovered something surprising as we’ve scaled: using a relatable tone and human voice are extremely important to proper support, but fast initial response and correctness have a much stronger correlation with customer satisfaction in a support interaction.

In practice, there’s a sliding scale effect. If your team immediately responds to customer tickets and solves customer problems, tone is less crucial because you’ve promptly mitigated risks. But if your team’s time to first response is long (24 hours or more), having an approachable and human tone is perhaps the only thing that can improve your relationship with the customer. In the worst possible scenario — taking an extremely long time to respond — you must have both great technical answers and an impeccable tone. This is the hardest response to achieve reliably. Given the option, encouraging and measuring a fast response time is the course of action that benefits most companies today.

### Takeaways

It’s hard to scale an effective support organization in the long term. You have to care about support and the customer experience more than you ever thought possible. You need to build tools and processes around support like you would your flagship product. Most importantly, you have to be willing to change your assumptions as your customer base scales and changes. The needs of your early customers will be very different than the needs of your later customers, but the care and respect you show them will be universal.

There’s not a lot of resources on scaling support available, but there is a great deal of writing on scaling operations, capacity planning, and structuring technical teams. Believe it or not, these may be the best resources for your company’s support needs. There are obviously some areas that don’t overlap; you should never treat your support team like interchangeable machines, for example. However, the process of planning based on business growth is a great mindset to use when architecting your support.

Most importantly, there’s a lot of non-advice about support out there. Telling your support team to “care more” or “engineer happiness” or “close more tickets” isn’t support leadership, as it’s not clear or actionable. Support is a process, like any other facet of building a company. You have to work at it, define your customer process effectively, and be pragmatic about what systems you need to scale. It’s not glamorous, but the sooner you can address your customer’s needs, the faster you can build a support organization that’s actually meaningful and helpful.

Scaling support can be difficult, but it’s not impossible. I shared our history at Fastly to give some insight into what it takes to build a great support infrastructure at your company. Fastly’s process will likely not fit your specific business needs, but hopefully our lessons learned can be of some benefit to you.
