---
title: "Voltage Drop, When does it Matter?"
date: 2026-08-15
summary: "You will not get the right voltage straight away if you don't have a _sense_ for it."
tags: [Power, Harness]
math: true
---

Whatever needs to be supplied by power on a spacecraft or on a testing setup, the voltage you apply at the supply is not what reaches your device: we need to compensate this effect.

## Principle
{: #voltage-drop-principle }

Let's go back to the formula $$ ... V=R_3\cdot I_1 $$

$$ V = R \times I_1 $$

Neither `history` over RS.

## Test Item

```
Highlighted text
```

{% include figure.html svg="retry-storm.svg" caption="Request rate at the caller during a 100% failure injection." %}

The p99 is not the number you want.[^tail]. See also [voltage-drop-principle](#voltage-drop-principle).

{% include figure.html src="/assets/img/voltage-drop/out.webp" alt="Request rate at the caller climbing 3x after the dependency starts failing" width="1200" height="860" caption="Load *increases* when capacity drops. Injection starts at t=40s." %}

## Resources

[^tail]: Dean & Barroso, *The Tail at Scale*, CACM 56(2), 2013. [Dean and Barroso showed](https://en.wikipedia.org/wiki/File:Apollo_Spacecraft_diagram.jpg)

## What to do instead

- Enjoy it
