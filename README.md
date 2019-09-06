# Quince
a 2.4 GHz SDR GreatFET neighbor using 1-bit ADCs

Required KiCad dependency:

https://github.com/greatscottgadgets/gsg-kicad-lib

If you are using git, the preferred way to install gsg-kicad-lib is to use the
submodule:

```
git submodule init && git submodule update
```

Quince is a GreatFET neighbor that serves as a Software Defined Radio (SDR) receiver for the 2.4 GHz band using a 1-bit sampling technique.  It is intended specifically to enable all-channel Bluetooth monitoring, but it should support additional uses.

Quince features the TLV3502 dual comparator and an RF section based on the AD8347 quadrature demodulator.  Synthesis of a 2.4 GHz Local Oscillator (LO) is provided by ADF4360-0.

A previous version of Quince lacked the RF section.  In addition to connecting to an [Azalea](Azalea), it plugged into the baseband header of HackRF One.  This permitted experimentation with a 1-bit ADC in conjunction with HackRF One's RF section.  The comparators converted the HackRF's differential analog baseband signals into logic-level signals sampled by Azalea's SGPIO peripheral.

Lower cost comparators that may have sufficient bandwidth:
* TLV3202, comparator, $0.60
* NCS2250, single, $0.20

It might be more cost-effective to use a wireless transmitter or transceiver IC to generate the LO, such as:
* CC2500
* ADF7242 (used on [Lucky Bamboo](Lucky-Bamboo))

As an alternative to the comparators (and possibly to the quadrature demodulator as well) we may investigate the use of LVDS input on an FPGA.
