# open_vettam_15CCT

Matter over Thread smart surface ceiling lamp project.

## What This Project Is

This is a hardware design for a smart tunable-white surface-mount ceiling lamp.
It includes:

- a main control PCB
- a dual-channel constant-current LED driver stage
- an LED MCPCB for CW and WW LEDs
- input protection and a local 3.3V supply for the controller

## Application

The product is intended to work as a smart ceiling light that:

- runs from a 24V LED power supply
- supports Matter over Thread control
- provides tunable white light using separate CW and WW channels
- uses PWM control to mix color temperature and dim brightness

## Hardware Summary

- Controller: ESP32-C6
- LED driver: TPS922053DRRR
- Buck regulator: LMR51610YDBVR
- Input rail: 24V
- LED configuration: 7 LEDs x 6 strings per channel
- Channels: CW and WW

## Main Files

- open_vettam_15CCT.kicad_sch
  Top-level control-board schematic
- 24v_Input.kicad_sch
  24V input protection
- 24-5_buck.kicad_sch
  24V to 3.3V buck supply
- MCU.kicad_sch
  controller section
- cc_driver.kicad_sch
  constant-current LED driver section
- led_mcpcb/
  LED board project
