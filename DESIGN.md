unfAPI Design
===

## Overview

There are multiple layers, specifically:

**TODO: Diagram**

All items within a layer should extend the base class provided in the related `base.py` file, and tests should go within the `tests/` folder for that layer.

## RF Drivers

The following are supported for alpha:

| Driver | RF Supported | Notes |
|--------|--------------|-------|
| KillerBee | IEEE 802.15.4     |
| GNU Radio SDR | IEEE 802.15.4 |

## Harnesses

These items are meant to allow control and monitoring of the target, in order to both:
- know when a target is in a valid or invalid state
- reset the device to a valid state (reboot, restart service, etc)

A user may select to use one harness for monitoring and another for reset, if appropriate.

The following are supported for alpha:

| Driver | Devices Supported | Notes |
|--------|--------------|-------|
| Arduino Serial | Arduinos | Uses an Arduino to monitor pin levels and capture serial from a target. Serial capture is less reliable than the FTDI based harness. |
| Serial | FTDI Adapters | Uses an FTDI adapter to process serial looking for specific messages. |
| RF Interface | Any RF Interface Supporting rx_poll

## Generators

This is where the fun comes in, to implement the fuzzing technique that you want to try against a target.
Typically you must only implement the `yield_test_case` and `yield_control_case` functions (plus any initialization code you need) in your class.

| Driver | RF Target | Notes |
|--------|--------------|-------|
| Isotope Preamble | IEEE 802.15.4  | Varies the number of nibbles in a preamble before a beacon request frame. See the Isotope paper for more detail. |
| Isotope Franconian Notch | IEEE 802.15.4  | Varies the values of nibbles in a preamble before a beacon request frame. See the Isotope paper for more detail. |
| Random Payload | IEEE 802.15.4 | Provides random content in a data frame. |
