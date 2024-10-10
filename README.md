# GPS-Rx-PPS
A KiCAD schematic and PCB to buffer/alarm a GPS receiver PPS signal

## Introduction

For a printable schematic, see the file:
- GPS Rx PPS_sch.pdf

For a file to send to a fabricator (eg JLCPCB or PCBWay), use the file:
- Fabrication/GPS Rx PPS.zip

## uBlox Receiver Configuration


## Circuit Description

The GPS receiver PPS signal is buffered by U2B to provide LED output, U2C to provide buffer drive for an external circuit, and the missing pulse detector built around U1. This will generate a low output after a few seconds of not receiving pulses; the timing can be adjusted by the combination of R3 and C4.


PCB Connections:
- CON1: DC Power in (5 V)
- CON2: Power LED
- CON3: Alarm LED
- CON4: PPS in, from GPS received (timing on falling edge)
- CON5: PPS LED
- CON6: PPS out (jumper selects low impendance or 50 Ohm)
- CON7: Alarm sounder out
