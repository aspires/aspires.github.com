---
layout: blog_post
title: 'How Fastly Builds Support, Part 1'
---

_Note: What started as a quick blog post about support [inspired by this tweet](https://twitter.com/austinspires/status/483435088546250753) 
quickly ballooned into a novella. The initial draft of this "quick blog post" 
was enormous, so I've  greatly edited down the content, and split the piece 
into multiple parts_

## Part 1: Our Standards

One of Fastly's greatest product advantages is our support infrastructure. We
get compliments and positive feedback nearly every day through tickets, tweets,
and old fashioned conversation. When we run case study interviews with customers,
support is a common factor in why people choose Fastly over other providers.
This is something we take pride in, and something we love to brag about.

This culture of support and service isn't an accident. Our support processes 
span the entire company, and are baked into every aspect of the way we do 
business. We worked hard to build our support infrastructure (our processes are 
so broadly encompassing and involved that calling our support an "infrastructure" 
is the only term that feels right) to scale without sacrificing quality, 
timeliness, or the soul that got Fastly where it is today.

In the time I've been at Fastly, we've had enough customers and friends ask us about
how we do support, and what's going on under the hood that it seems appropriate
to give a high level overview of how we build, what we've learned, and what other
teams can borrow/steal from our setup.  

## The Context

When you look at Fastly's support, you have to start with looking at the context
surrounding the company.

Infrastructure vendors historically have bad support experiences, unless
you're spending something huge: think budgets in the tens of millions. Even then, support
is viewed as a cost center -- the vendor's goal with support is for you to go
away. If you going away is the result of them solving a problem, that's a plus.
But the goal is to make you go away, solution or not. If you don't believe
me, talk to your head of ops.

Because we're a company founded by operations engineers, for operations engineers,
having par-for-the-course (ie: bad) support wasn't acceptable. Fastly's founding
team set out to create the support experience they always wanted from a vendor.

The catch is: every startup begins with this goal. I've never met a business owner who
feels like their company should have bad, or even mediocre, support. They all claim
they want the best. That said, we've all seen cases where companies grow, become
successful, and their support inevitably goes down the tubes. That pursuit of
"the best" has been sacrificed, either intentionally or as an unfortunate side
effect of other decisions.

I can't comment on other companies and their circumstances, but I can go into
detail about the culture and processes that Fastly has in place to prevent this.

## The Early Days of Yore

In the earliest days of Fastly, the team made some very crucial decisions about
how they would approach support as a company.

From the outset, support was considered a profit center, rather than a cost of
doing business. Fastly theorized that great support would generate more
business than any sales force could in the earliest days, and approached setting up
support with that in mind. It turns out, that theory was right, and customers
flocked.

In the operations world, reputation is everything. Fastly already had respect in
the community through the early team's technical reputation, but their support
reputation became world renowned in quick fashion.

So, what actual decisions were made to set the foundation?

In the early days of Fastly, everyone joined in on support. Engineering, Ops,
Neteng: they all took tickets they could answer, helped as quickly as possible,
and communicated as honestly as they could.

Everyone shouldered the support burden, and took pride in delivering a great
experience. The experience was so valued that people even "competed" to take
tickets first. Great support was baked into the culture. Fastly's early
employees had all run into horrible vendor support in their previous jobs, and
were determined to do the opposite in their time at Fastly.

The people who shipped product answered the tickets about their features, wrote
docs as needed, and made sure customers got the full benefit of Fastly. When
new customers came in, everyone pulled together to make sure the migration went
smoothly. It wasn't farmed out to a specific individual, the customer wasn't
just left to their own devices. Infrastructure migration often needs extra help to
make the process go well, so everyone chipped in. The customer's success was
viewed as Fastly's success.

A buzzphrase in the startup community these days is "do things that don't scale."
Fastly did this with support. It's not scalable to have your entire team onboard
single customers. It's not scalable to have your CEO assist in real time over IRC.
It's not scalable to give your everything to make sure the customer has a great
experience.

The catch is: during those same early days, _we did start scaling_, and we did
so very successfully. We started building the tools, resources, and everything
else necessary to make sure this quality could be extended indefinitely into the
life of Fastly.

It was said earlier: Fastly is a company by operations engineers, for operations
engineers. Ops scales applications. Ops plans capacity. Fastly scaled and planned
for capacity with support in this same way.

As an aside, many support teams are avoiding the concept of "scaling support"
outright, as "scaling support" often implies cutting corners and removing the
human touch that makes so many organizations successful. This should more
accurately be considered "scaling support poorly." When Fastly scales support, we
make the conscious effort to preserve the most essential facing aspects. If those
aren't preserved, we view the scaling efforts as a failed (but valuable) test
and roll back.

---

The next part of this piece will go into the decisions we made early on as an
organization, the lessons we learned in the process, and what we've done to expand our quality 
of support and customer service. [Follow me on twitter](https://twitter.com/austinspires) 
to hear when updates are live!
