---
title: Inter-Integrated Circuit (I²C)
weight: 230
tags: ["I2C"]
---

## What is it?

I²C (spoken as I-Squared-C) is a bus originally invented by Philips. 
It is designed as a classic master-slave bus. A data transfer is always i
nitiated by a master. It can also be set up in a multi-master system. 
I²C is connected via two signal lines (data line and clock line). 
The transmission rate of the bus can be between 0.1 Mbit/s up to 3.4 Mbit/s 
depending on the clock rate. If only a unidirectional connection is required, 
even 5.0 Mbit/s would be possible. It should be noted: the higher the clock rate, 
the more susceptible to failure the overall system becomes. The low operating 
voltage of only 3.3V does not contribute to interference resistance either.

## Uses

I²C is mainly used for communication between microcontrollers. The advantage 
that a whole series of microcontrollers can be controlled via just 2 lines is 
of course very interesting for the circuit board layout. The main advantages of 
I²C are its simplicity. There are certainly newer bus systems with better 
transmission rates. Hardly any bus system is as easy to use as I²C. Even 
“hot plugging”, ie plugging in and unplugging the devices during operation, 
is possible with I²C.

## Addressing

I²C uses an address space of 7 bits. This allows up to 112 nodes on one bus. 
The remaining 16 addresses are reserved for special applications. Usually the 
address of a device is defined directly by the manufacturer. It can therefore 
be found in the relevant data sheets. Due to the shortage of addresses, 
there is also a variant with a 10-bit address space. Up to 1136 nodes are 
possible, and the protocol is compatible with the smaller 7-bit address space.

## Transfer rates

| Mode | Max. transfer rate | Direction |
| --- | --- | --- |
| Standard Mode | 0.1 Mbit/s | bidirektional |
| Fast Mode | 0.4 Mbit/s | bidirektional |
| Fast Mode Plus | 1.0 Mbit/s | bidirektional |
| High Speed Mode | 3.4 Mbit/s | bidirektional |
| Ultra Fast-mode | 5.0 Mbit/s | unidirektional |

## Additional information
- [Wikipedia I²C](https://en.wikipedia.org/wiki/I%C2%B2C)
- [I²C Bus](https://i2c-bus.org)

{{% notice warning %}}Please be aware there are some hardware issues when using the Raspberry Pi with devices that expect 
to be able to use clock stretching, for more info see 
["Adventures in I2C: clock stretching on the Raspberry Pi"](https://www.recantha.co.uk/blog/?p=19880) 
and ["I2C stretch bug. Been fixed or not?"](https://www.raspberrypi.org/forums/viewtopic.php?t=220428).{{% /notice %}}
