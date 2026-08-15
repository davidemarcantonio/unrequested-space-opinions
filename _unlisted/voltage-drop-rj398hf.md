---
title: "Voltage Drop, When does it Matter?"
date: 2026-08-15
summary: "You will not get the right voltage straight away if you don't have a 'sense' for it."
tags: [Power, Harness]
math: true
---

Whenever a device needs to be supplied power, the (constant) voltage, also called [direct current "DC"](https://en.wikipedia.org/wiki/Direct_current) voltage, you apply at the power supply is not what reaches the device: one needs to compensate this effect to get the desired voltage at the device. This happens in general and as well on a spacecraft or on a testing setup.

## Votlage Drop Principle
{: #voltage-drop-principle }

Let's start from [Ohm's law](https://en.wikipedia.org/wiki/Ohm%27s_law) $ V=R\cdot I $

$$ V = R \times I_1 $$

{% include figure.html src="/assets/img/voltage-drop/schematic.webp" alt="Voltage drop circuit diagram" width="1200" height="900" caption="Voltage drop *circuit diagram*" %}


```
So the `voltage drop` depends on the current and on $$ R_L $$.
```

## Example

{% include figure.html svg="retry-storm.svg" caption="Request rate at the caller during a 100% failure injection." %}

- See [^voltage-drop-wiki]. 
- See also [voltage-drop-principle](#voltage-drop-principle).

## Resources

A [spreadsheet](https://docs.google.com/spreadsheets/d/1rzpiZibkyrv44S69Ek5TSALbYB5_mABpBpv2OOpHTSo/edit?usp=sharing) with the formula that allows to derive voltage drop.

[^voltage-drop-wiki]: [Voltage Drop, Wikipedia](https://en.wikipedia.org/wiki/Voltage_drop)


