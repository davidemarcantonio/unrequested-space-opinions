---
title: "Voltage Drop, When does it Matter?"
date: 2026-08-15
summary: "You will not get the right voltage straight away if you don't have a _sense_ for it."
tags: [Power, Harness]
math: true
---

Whatever needs to be supplied by power on a spacecraft or on a testing setup, the voltage you apply at the supply is not what reaches your device: we need to compensate this effect.

## Principle
{: #voltagedropprinciple }

Let's go back to the formula \( ... V=R\_3*I\_1 \)

$$ V = R \times I_1 + I\_1 $$

Neither `history` over RS.

## Test Item

```
10\times log_10 ≈ 18%
```

{% include figure.html svg="retry-storm.svg" caption="Request rate at the caller during a 100% failure injection." %}

The p99 is not the number you want.[^tail]

## Resources

[^tail]: Dean & Barroso, *The Tail at Scale*, CACM 56(2), 2013.

## What to do instead

- Enjoy it
