---
title: Logging
summary: When you should and shouldn't log stuff
author: David Cox
publishDate: 2018-08-19
layout: post.njk
---

For the uninitiated, in the realm of software, "logging" refers to the process
of writing out chunks of data while a piece of software is running. This data
can be writing out for any purpose, but common reasons include record keeping
(that may help fulfill compliance obligations) and operational insight (knowing
that things are running well and debugging issues when they occur).

I'm pretty opinionated when it comes to software logging in a production
environment. If it can be logged, I want it logged. The more logs the better.

In practice, this isn't always practical. The more logs you have coming out of
your system, the more you have to sift through to find the ones you're
interested in. Additionally, logs take up space - and while storage space is
getting cheaper these days, it's not free.

The best thing you can do about noisy logs is utilize a log management system
(like Splunk or an ELK stack). It allows you to filter and sort your logs in any
number of ways, making it much easier to understand what's being reported. Once
you've got a handle on how the management system works, additional logs can
actually be preferable to fewer. With more logs it's easier to identify
precisely where things are going wrong in your code, making debugging so much
easier.

Eventually your logs will start to fill up disk space. When that time comes
there are only so many things you can do. You can pay for more disk space or get
rid of some logs.

More disk space doesn't have to scale linearly. When your logs are sufficiently
old you're not likely to need to sift through them often (if at all). You can
store your old logs in a slow, cheap storage option and hope you'll never need
to access them.

If you're willing to bet more on never needing to access your old logs, why not
just delete them? Some organizations will need to keep these logs around for
compliance, but many can just dump them. Many log management systems will make
this easy to do - automatically purging logs when they reach a certain age.

These log burden mitigation strategies won't work for every organization. For
those, reducing overall log production is a must. This is not something to take
lightly. Reduced log production makes debugging harder and will likely affect
future system development.

Occasionally someone will suggest turning off certain types of logs until a
problem arises. This can be accomplished through adjusting log severity levels
or turning off the logger for certain system components entirely. This sounds
good in theory, but I have my doubts.

In debugging a system, you often don't know what information is relevant until
you've dug into an issue for a while. Filtering out information ahead of time
will potentially leave out some critical details, handicapping the process.
Furthermore turning up the logging after a problem occurs misses the most
important information. When finding the root cause, it's important to know how
the problem started - not just how the latest occurrence was manifested.

Set up a healthy log infrastructure. Once you're in need of those details you'll
be glad you took the time.
