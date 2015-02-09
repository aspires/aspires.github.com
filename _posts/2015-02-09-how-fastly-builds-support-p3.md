---
layout: post
title: "How Fastly Builds Support, Part 3"
---
_This is the third part of a multi-part series on how Fastly architects and
builds our support process. You can read [part one](http://aspires.github.io/2015/01/05/How-Fastly-Builds-Support-p1/) and [part two](http://aspires.github.io/2015/01/12/How-Fastly-Builds-Support-p2/) to get prior context._

Fastly has made some key decisions about how to operate and structure our support team in a way that allows us to deliver quality at scale. Some of the lessons we learned are more specific to issues we encountered as we grew, but most can be applied to any support or customer-facing team.

###Don't repeat yourself
The first support pain point Fastly ran into was answering repeated 
questions, as every company might experience. There are two major tactics
that can be used in some combination for solving this problem: documentation and
canned scripts in the ticketing system (or a text expander tool). Adding people to
the team is a solution, too, but that isn’t possible for many companies,
as it's by far the most expensive and least efficient way to address the 
problem.

In true ops fashion, Fastly embraced DRY (Don't Repeat Yourself) in full force.
If a question was asked twice, someone built the answer into a document on docs.fastly.com. The team didn't use canned scripts or macros at all. The nature of our questions
didn't make reusable scripts practical -- even today there are not a lot of canned
scripts used due to the nature of our support requests.

This presented a few issues. Sometimes the docs were unorganized, as nearly
every employee contributed, and sometimes the docs overlapped. At the time,
there was no one owning or coordinating documentation efforts.

But, it was a net positive, as it tapped into a support truism: __many people
would rather not contact support at all__. If you can make it easier for your 
customers to self service, you're making it easier for everyone. It also makes 
it possible for customers to solve problems themselves, which makes them 
feel awesome. And who doesn't like feeling awesome?

It's important to note that when a customer contacts support, they are taking a lot of effort to seek assistance and admit they need outside advice. For some people,
that's a normal process. But for others, it can be a huge ego hit. If you can
make self-service easier, either through product design or documentation, your
customers will have a better experience with your product, which directly shapes
their support experience.

### The right tools for the job
Another friction area Fastly encountered early on was the need to 
communicate through more than just email or support tickets. Since 
everyone in the company (and most of our early customer base) was already in 
IRC, it made sense to set up an IRC room for customer communication. 
The room `#fastly` on Freenode was born. It's still there. You can ping me in 
there right now, most likely (I'm @aspires).

IRC is an amazing way to communicate with customers in real time to either debug
problems or talk shop. You'll get some of your best feature requests and 
product insights from the users who take the time to chat with you. Also, Fastly
has reached a critical mass where customers are helping other customers. That's
amazing, but it's not unique to us. It’s happened at every company I've seen with a maintained IRC room.

IRC helps us scale in another way. When we're working closely with
customers, we can set up rooms for the customer quickly, and get down to work
without a lot of overhead. Customer onboarding for major infrastructure changes 
needs to be faster and smoother than email, but not as time-consuming and cumbersome as a conference call. IRC offered an ideal, asynchronous communication tool that only 
chat can provide.

We later found that when customers helped other customers in IRC, a lot of shared knowledge wasn't getting logged in a reusable way. So,
we've recently launched a Discourse-powered Community forum to help keep the interesting 
use cases and shared knowledge in an indexed location.

We also have a lot of unique workflow-improving tools for our specific
circumstances. Some are built right into our ticketing system, and others live 
in a central location outside of the ticketing system. Nearly every support 
team has them, so this isn't a huge surprise. But I do recommend building these
as early as possible. A great support toolset, combined with comprehensive
documentation, will scale your support organization more than you think. It's
also fun to blow off some steam hacking on an internal tool that will get real
use.

Another tool we use heavily at Fastly is our pager system. That's right, support
carries a pager. It's a follow-the-sun rotation with our London office, which
eliminates the risk of being woken up. It originally started as a way to track
who would field tickets over the weekends, but we've applied the rotation to
different tasks. For example, we have Premium Support customers with an
emergency trigger email, which pages our support team. It also means that if there's an issue that needs support assistance, our engineering teams have the ability to page us.

### A dedicated department
I said earlier that Fastly started out with engineering answering tickets 
directly. It was a great process that helped fine-tune our initial product set 
in the best way possible. Fastly was able to make this scale further than most. With the techniques and tools previously outlined, Fastly engineering was 
able to do their own support for almost two years without a dedicated support 
organization.

But, as ticket load increased, and as teams across Fastly began to specialize, 
there came a time to build a real support team. Fastly has structured support as
part of a larger organization called Customer Engineering, responsible for the
entire customer onboarding and lifecycle process. This includes sales 
engineering, support, documentation, and professional services. Some teams call 
this "Customer Success," but the result is the same -- support is factored into 
the entire business process, rather than operating as an outside team.

Fastly officially started the customer engineering team in mid-2013 with 
support being the primary responsibility, but the team took on sales engineering
work that was previously done by the founders and a few early employees. At the time of writing, Fastly's customer engineering team has nearly 20 people divided among our SF, London, and NYC offices.

### Team structure
That leads into team structure — not just how our support organization is
structured, but how we interact with the rest of the company.

Customer engineering is a first-class organization at Fastly that actively works
with all teams to ensure a high-quality customer experience. We have the
resources we need to grow and make decisions for the good of the customer, and 
because we're structured to address the entire customer cycle, we can have real 
impact on customer happiness and product perception.

The customer engineering organization is also included in the product 
development process. We don't dictate what's happening, but we do 
get copied on projects as they progress. Because we're looped in regularly, 
we're set up for success; things don't ship as a surprise, and when things do 
ship, we've done the necessary work to be ready for go-live. Because of this,
we're better prepared to manage inevitable bug reports and customer issues after
ship.

This is critical for good support and happy customers -- simply looping your 
support team in on the development process early will make your ships 
significantly more successful than pushing features without communication.

Fastly's process for solving tickets with other departments is also unique. Typically, support organizations operate on their own island, where they 
either cannot escalate a ticket to product engineering for assistance (the 
common startup scenario), or where they escalate a ticket to a magical "next 
level," never to see it again (the common big company scenario). Neither of these
is ideal. You're either building a system where customers run into barriers and
red tape, or a system where support pushes the buck to other people.

Fastly intentionally structures its support workflow in the following way for
escalating and interacting with other teams:

1. New ticket comes in.
2. Support claims the ticket and starts investigating.
3. Support comes to a point where another team needs to weigh in.
4. Support assigns the ticket to the team's group in the ticketing system (support is still copied on the ticket, as well).
5. The assigned team is now responsible for providing an answer, update, or response on to the ticket thread.
6. Someone from the assigned team weighs in, possibly responding to the customer directly.
7. Support takes the ticket back, and continues solving the issue. At this point, if necessary, go to #4 and repeat.
8. Support resolves the issue with the customer.
9. Support starts the documentation process as needed.

It's a little more involved than other organizations, but the important steps
here are #5 and #7. When support assigns a ticket to another group, such as ops,
finance, legal, neteng, etc., that team works to get an update as soon as they 
reasonably can. Once that team weighs in, it’s support's job to take that, relay 
it in a meaningful way to the customer, ultimately resolve the issue, and create
documentation (if appropriate).

Our technical teams have been experimenting with an "on call" rotation for 
interfacing with other teams on pressing issues. Fastly just happened to use 
pager shifts like this to structure other things, so it made sense to build 
support (and other teams) into the shift process for communications. You may 
need a different system, but the main point is this: great support teams need to have
a codified way to work with the rest of the company in a way that doesn't 
distract or derail daily work.

If support isn't included in the final process of shipping products, and 
if your support organization doesn't have a respected way to pull in other teams
 to help solve customer problems, you're hindering your efforts to build and 
scale the quality of support you offer. The people who end up suffering are
your customers and users. 

This piece definitely got more into the trenches of planning, team management, 
and the actual process of growing support. So if you have any follow-up 
questions, let me know at [@austinspires](twitter.com/austinspires) on Twitter. 

There’s one post more left in this four-part series, so stay tuned.
