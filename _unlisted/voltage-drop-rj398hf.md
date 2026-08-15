---
title: "Voltage Drop, When does it Matter?"
date: 2026-08-15
summary: "You will not get the right voltage straight away if you don't have a 'sense' for it."
tags: [Power, Harness]
math: true
---

* Assuming a constant voltage provided by the power supply, also called [direct current or "DC"](https://en.wikipedia.org/wiki/Direct_current) voltage
* Anything in between the power supply and the device would lower the actual voltage seen by the device due to its resistance
* This can be compensated with "sense" functions in power supplies with some limitations

## Votlage Drop Principle
{: #voltage-drop-principle }

See [^voltage-drop-wiki], let's start from [Ohm's law](https://en.wikipedia.org/wiki/Ohm%27s_law)

$$ V = R \times I $$

The current draw will depend on the overall DC resistance (sometimes called DCR) which is tipically dominated by the load resistance while the resistance in between is tipically due to cable resistance and is small.

$$ I = \frac{V_supply}{R_tot} $$

$$ R_tot = R_L + R_H1 + R_H2 \approx R_L $$ since $$ R_H = R_H1 \approx R_H2 $$ and $$  R_L >> R_H $$

So, the drop is 

$$ V_drop = I \cdot R_H1 + I \cdot R_H2 = 2 \cdot I \cdot R_H$$

and the voltage at the load is

$$ V_L = V_supply - V_{drop} $$

See an example in [voltage-drop-example](#voltage-drop-example).

{% include figure.html src="/assets/img/voltage-drop/schematic.webp" alt="Voltage drop circuit diagram" width="900" height="1200" caption="Voltage drop *circuit diagram*" %}

```
The `voltage drop` depends on the current which in turn depends on the load resistance.
```

## Example
{: #voltage-drop-example }

- A [spreadsheet](https://docs.google.com/spreadsheets/d/1rzpiZibkyrv44S69Ek5TSALbYB5_mABpBpv2OOpHTSo/edit?usp=sharing) with the formula that allows to derive voltage drop.

|                    | Unit | Value |  Source  |
|--------------------|:----:|:-----:|:--------:|
| Power supply Voltage            |   V  |  5.00 | Input    |
|                    |      |       |          |
| Harness one way resistance |  Ohm |  0.2  | Input    |
|                    |      |       |          |
| Device (Load) Resitance           |  Ohm |  2.4  | Input    |
|                    |      |       |          |
| Current            |   A  |  2.08 | Computed |
|                    |      |       |          |
| Voltage Drop       |   V  |  0.83 | Computed |
|                    |      |       |          |
| Voltage at Device  |   V  |  4.17 | Computed |


## Sense Function

TBW

## Power Supply Limitations

Keysight example with 2 V compensation

## Multiple Wires Solution and Formulation

TBW


## Resources

- [^voltage-drop-wiki]: [Voltage Drop, Wikipedia](https://en.wikipedia.org/wiki/Voltage_drop)


