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

## Properties of a balun

### Impedance ratio

The impedance ratio is:
 * The square of the turns ratio
   * ie. 4:1 impedance ratio corresponds to a 2:1 turns ratio.
 * The ratio of impedance betweeen the balanced and unbalanced sides.
   * ie. a 4:1 ratio balun with 50 ohm impedance on its unbalanced coax feed line would have 200 ohms impedance on the balanced antenna lines.

### Types of Baluns

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

"The best balun to use is the one that does the job with the least loss, of course."

There are two main design approaches:
 * Antenna line integral approaches.
 * Discrete component based approaches.

In selecting a design approach, you have to consider:
 * Whether you have a dedicated antenna
 * What bandwidth is required
 * What the operating frequency will be

Generalities:
 * For wavelengths over 6m, dedicated antennas are generally used. If you have a dedicated antenna, then you can produce an efficient balun as an antenna line integral approach, such as a half-wave loop. Such an approach is classified as a voltage balun.
 * In situations where a wide bandwidth is desirable, voltage baluns are generally too big or too inefficient. If you use a tuner, that does all the impedance matching necessary so a simple current balun after an unbalanced tuner has the lowest insertion loss. In this situation a current balun is best.
 * If a wound balun with impedance matching is needed, the auto-transformer types are generally more efficient.

If you are creating a discrete component based balun, then you have to decide whether you want a design that can be reliably reproduced, or you want to hand-tweak.
 * If hand tweaking, you can "roll your own" by wrapping wire around a magnetic core. Considerations include selecting a core material, a wiring strategy, a wire diameter, and a wiring topology.
 * If interested in a reproducible design, then you want to look at a combination of available SMT and through hole components and on-PCB solutions.

## Immediate requirement

Currently we are interested in solutions for [adxi](https://github.com/vk2diy/adxi) antennas, which is to say 5W intended power at 12V nominal.

Roughly speaking,this is 0.4A, however we should assume some margin to account for resonance (voltage up to 100V), transients, etc. and look for higher current ratings in the selected components.

The initial frequencies to test are the 20m, 30m and 40m HAM bands.

The feed lines will be 50 ohm coax.

The best baluns for these frequencies may be calculated as follows:
 * ...


## References

 * [Coilcraft *A Guide to Understanding Common Mode Chokes*](https://www.coilcraft.com/en-us/edu/series/a-guide-to-understanding-common-mode-chokes/)
 * [Marki Microwave *Balun Basics Primer*](https://e2e.ti.com/cfs-file/__key/communityserver-discussions-components-files/14/balun_5F00_basics_5F00_primer.pdf), Marki Microwave, Inc. (2014)
 * [Murata *Basics of Noise Countermeasures [Lesson 6] Common mode choke coils*](https://article.murata.com/en-global/article/basics-of-noise-countermeasures-lesson-6) (2011)
 * [XE3RLR](https://www.qsl.net/xe3rlr/balun.htm)
 * [VK5AJL](http://www.vk5ajl.com/projects/baluns.php)
