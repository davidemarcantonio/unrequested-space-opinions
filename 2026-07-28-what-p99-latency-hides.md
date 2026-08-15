---
title: "What p99 latency hides"
summary: "A percentile is a summary, and every summary throws something away. Here is what the p99 throws away, and when that matters."
tags: [performance, observability]
---

Percentiles are the standard way to talk about latency, and mostly that is
a good thing: a mean latency of 40 ms tells you almost nothing when the
distribution has a tail. But the p99 is still a summary, and summaries are
lossy by construction.

## Averaging percentiles is not a thing

The failure I see most often looks like this: each service instance reports
its own p99, a dashboard averages them, and the number on the wall is
presented as "our p99."

It isn't. Percentiles are not linear, so you cannot average them and get
the percentile of the combined population.

```
instance A: 1000 requests, p99 = 20 ms
instance B: 10   requests, p99 = 900 ms

mean of the two p99s = 460 ms
true p99 of all 1010 requests ≈ 22 ms
```

Neither number is wrong about its own population. The mean is just not
answering the question anyone asked. To combine, you need the underlying
distribution — a histogram with shared bucket boundaries, which is exactly
what Prometheus `histogram_quantile` over a `_bucket` metric gives you.

## One user, many requests

The second thing the p99 hides is that users do not issue one request.

If a page load fans out to 20 backend calls, and each call independently
has a 1% chance of being slow, then the probability that a page load
touches at least one slow call is:

```
1 - 0.99^20 ≈ 18%
```

So a "99th percentile" backend translates to something closer to a
**82nd percentile** page. This is the argument behind tail-tolerant design:
hedged requests, request-level timeouts that are shorter than you'd think,
and fanout budgets.

## What to do instead

- Export histograms, not pre-computed quantiles, and aggregate at query time.
- Track the tail you actually care about. If your SLO is on page loads, measure page loads.
- Watch p99.9 as well as p99. The difference between them tells you the shape of the tail.
- Keep a max. It is a terrible statistic and an excellent alarm.

None of this makes percentiles bad. It makes them a starting question
rather than an answer.
