---
title: "Retries are a load multiplier"
summary: "Retrying a failed request is the obvious fix, and under the exact conditions where you need it most, it is also how a partial outage becomes a total one."
tags: [distributed-systems, reliability]
---

Retries are the first resilience pattern everyone adds and the last one
anyone tunes. The uncomfortable property: a retry policy behaves fine
while the system is healthy and turns hostile the moment it isn't.

## The arithmetic

Suppose a service is degraded and failing 50% of requests. With three
attempts per logical request, callers now issue roughly 1.75 requests for
every one they'd normally send. Degrade further to 90% failures and that
climbs toward 2.7. Load goes *up* precisely when capacity has gone *down*.

Stack that across a call chain and it compounds. Three services deep, each
retrying three times, and one slow leaf gets 27 attempts per user action.

## What actually helps

**Retry budgets.** Cap retries as a fraction of total traffic — say 10%.
Under normal conditions the budget is never exhausted; during an outage it
puts a hard ceiling on the multiplier. This is more robust than tuning the
per-request attempt count, because the limit is defined against the thing
you care about.

**Backoff with jitter.** Exponential backoff alone still synchronises
clients into waves. Full jitter breaks that up:

```python
def backoff(attempt, base=0.1, cap=10.0):
    return random.uniform(0, min(cap, base * 2 ** attempt))
```

**Retry only what is retryable.** A 400 will fail identically the second
time. A 503 with `Retry-After` is telling you something specific. Treat
timeouts with care: you don't know whether the write landed, which is an
idempotency question, not a retry question.

**Circuit breakers as the outer bound.** When a dependency is clearly
down, stopping is better than politely backing off. Fail fast, shed load,
let it recover.

## The test worth running

Take a staging dependency, make it fail 100% of requests, and watch the
request rate at the caller. If the graph goes up, you have a load
multiplier, not a resilience pattern.
