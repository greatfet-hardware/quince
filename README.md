# Quince
a 2.4 GHz SDR neighbor for GreatFET using 1-bit ADCs

Quince is a GreatFET neighbor that serves as a Software Defined Radio (SDR) receiver for the 2.4 GHz band using a 1-bit sampling technique.  It is intended specifically to enable all-channel Bluetooth monitoring, but it should support additional uses.

Quince features the TLV3502 dual comparator and an RF section based on the AD8347 quadrature demodulator.  Synthesis of a 2.4 GHz Local Oscillator (LO) is provided by ADF4360-0.  The 1-bit quadrature signals are sampled at 80+ Msps by the SGPIO peripheral on [Azalea](https://github.com/greatfet-hardware/azalea).

Channelization and demodulation are done in software on the host computer, but it may be necessary to add an FPGA to Quince in order to achieve real-time simultaneous monitoring of all Bluetooth channels.  The host software will likely be a rewrite of [gr-bluetooth](https://github.com/greatscottgadgets/gr-bluetooth) using [libbtbb](https://github.com/greatscottgadgets/libbtbb) (the core of software for [Ubertooth](https://greatscottgadgets.com/ubertoothone/)).

## Project Status

The first hardware prototype that achieves proof-of-concept has been assembled.  Software work is required before determining what changes are needed in the next hardware revision.

## Viewing or Modifying the Design

Required KiCad dependency:

https://github.com/greatscottgadgets/gsg-kicad-lib

If you are using git, the preferred way to install gsg-kicad-lib is to use the
submodule:

```
git submodule init && git submodule update
```

## Hardware Development Notes

Lower cost comparators that may have sufficient bandwidth:
* TLV3202, comparator, $0.60
* NCS2250, single, $0.20

It might be more cost-effective to use a wireless transmitter or transceiver IC to generate the LO, such as:
* CC2500
* ADF7242 (used on [Lucky Bamboo](https://github.com/greatfet-hardware/luckybamboo))

As an alternative to the comparators (and possibly to the quadrature demodulator as well) we may investigate the use of LVDS input on an FPGA.  This would be the preferred solution if an FPGA ends up on the board anyway for channelization.
