# GPS-Rx-PPS
A KiCAD schematic and PCB to buffer/alarm a GPS receiver PPS signal

## Introduction

There are many cheap GPS receiver boards available which provide a serial output and Pulse-Per-Second (PPS) output, typically based on the uBlox 6 or later chip. This board is designed to take the PPS signal from such a receiver and provide buffering, LED drive, and missing pulse alarm (audio and LED).

For a printable schematic, see the file:
- GPS Rx PPS_sch.pdf

For a file to send to a fabricator (eg JLCPCB or PCBWay), use the file:
- Fabrication/GPS Rx PPS.zip

## uBlox Receiver Configuration

The uBlox receiver can be configured via the serial line using the [uCenter](https://www.u-blox.com/en/product/u-center) software. It should generate a 1 Hz outout (timed on falling edge) when GPS synchronisation has been obtained, otherwise a constant high to indicate failure:

View -> Configuration View; to activate change: Send

- TP5 (Timepulse 5)
    - PPS Settings for no GPS lock (eg use as an "alert" signal:
        - Frequency : 1 Hz -> 10 Hz
        - Duty Cycle : 100% -> 25% (alternatively set to 0% for permanent low output)
    - PPS Settings for GPS Locked:
        - Frequency Locked : 1 Hz
        - Duty Locked : 50%
    - Rising Edge on TOS

To save:
- CFG (Configuration)
    - Select: Save current configuration
    - Select in Devices: 2-I2C-EEPROM

## Circuit Description

The GPS receiver PPS signal is buffered by U2B to provide LED output, U2C to provide buffer drive for an external circuit, and the missing pulse detector built around U1. This will generate a low output after a few seconds of not receiving pulses; the timing can be adjusted by the combination of R3 and C4.

U2D and U2E provide an audio oscillator of a few kHz; its frequency can be adjusted by R9 and C6 to match the resonant frequncy of the piezo sounder used. The oscillator use U2F as an output buffer/drive, with RV1 preset setting the desired volume.
The oscillations are quenched when Q2 is turned on, ie when the "Not Alarm" output of U1 is high.

PCB Connections:
- CON1: DC Power in (5 V)
- CON2: Power LED
- CON3: Alarm LED
- CON4: PPS in, from GPS received (timing on falling edge)
- CON5: PPS LED
- CON6: PPS out (jumper selects low impendance or 50 Ohm)
- CON7: Alarm sounder out
