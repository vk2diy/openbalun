# openbalun

This repository is for open hardware balun designs.

There are two types of baluns, __current balans__ and __voltage baluns__.

We will focus on the more useful __current baluns__.

## Definition

A balun is any three port device with a matched input and differential outputs. It is most succinctly described by the required (ideal) S-parameters:

```
S12 = -S13 = S21 = -S31
S11 = -∞
```

Note what is implied by this:
 * A balun is a three port power splitter, similar to a Wilkinson or resistive power divider.
 * The two outputs will be equal and opposite.
   * In the frequency domain. this means the outputs have a 180° phase shift.
   * In the time domain, this means the voltage of one balanced output is the negative of the other balanced output.
 * The unbalanced input is matched to the input transmission line impedance (usually 50 Ω).
 * Unlike an isolator or circulator, a balun is a reciprocal device that can be used bidirectionally.

## Impedance ratio

The impedance ratio is:
 * The square of the turns ratio
   * ie. 4:1 impedance ratio corresponds to a 2:1 turns ratio.
 * The ratio of impedance betweeen the balanced and unbalanced sides.
   * ie. a 4:1 ratio balun with 50 ohm impedance on its unbalanced coax feed line would have 200 ohms impedance on the balanced antenna lines.

## Types of Baluns

 * __Flux coupled balun transformer__
   * Most common type, generally implemented as a transformer
   * Only really useful beneath 1GHz
   * Two wires are wrapped around a magnetic core
   * One side of the primary winding is grounded
   * The result is an unbalanced condition on the primary side, and a balanced condition on the secondary side
   * The ratio of turns defines the impedance ratio
 * __Other types of coupled line baluns__
   * Tapered microstrip transmission line balun, Marchand balun, coplanar wave guide balun, coaxial balun, planar transformer (spiral) balun, etc.
   * Mostly used from 500MHz upward, in part because 1/4 wavelengths are too long at lower frequencies

## Design decisions

In selecting a design appraoch, basically, you have to decide whether you want a design that can be reliably reproduced, or you want to hand-tweak.

If hand tweaking, you can "roll your own" by wrapping wire around a magnetic core.

If interested in a reproducible design, then you want to look at a combination of available SMT components and on-PCB solutions.

## References

 * [Balun Basics Primer](https://e2e.ti.com/cfs-file/__key/communityserver-discussions-components-files/14/balun_5F00_basics_5F00_primer.pdf), Marki Microwave, Inc. (2014)
 * [XE3RLR](https://www.qsl.net/xe3rlr/balun.htm)
