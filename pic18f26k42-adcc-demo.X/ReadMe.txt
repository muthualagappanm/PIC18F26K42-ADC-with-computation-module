
ADCC Demo ReadMe file
Author: C. Best
Microchip Technology, Inc
MCU8 Applications

This file describes the ADCC Demo.

Hardware used:
            *Microchip Curiosity HPC Demonstration Board
            *PIC18F26K42 8-bit microcontroller
            *MCP2220 USB to UART Demonstration Board
            *Voltage setting jumper set to 3.3V

Software used:
            *MPLAB X IDE v.4.10
            *XC8 C-Compiler v1.45
            *MCC plug-in tool v3.45.1
            *PC terminal program (Tera Term)

[Link to a relative file ](device_config.mc3)

[Link to a relative file path from root](/pic18f26k42-adcc-demo.X/nbproject/project.xml)

[Link to a relative file path from root Incorrect](/PIC18F26K42-ADC-with-computation-module/pic18f26k42-adcc-demo.X/nbproject/project.xml)

[Link to a relative file with ./ ](./device_config.mc3)

## Objective:

![Absolute External URL](https://static.transim.com/img/52018/5a411f3921b1452eaf5a9c97f9928980-7l7d1.jpg)

### Relative file path to root:

![Relative URL to root](/images/mcc/bits.png)

### Relative file path:

![Relative file path](/adapter.png)

### Relative file path with ./:

![Relative file path](../images/mcc/bits.png)

### Relative Incorrect:

![Relative Incorrect](/PIC18F26K42-ADC-with-computation-module/images/mcc/bits.png)

Operation:

The demo uses the 28-pin PIC18F26K42 microcontroller placed into the HPC demo board's 28-pin socket. 
The MCP2200 demo board's TX output must be connected to the PIC's RC6 (TX) output, and the MCP2200 
GND must be connected to the HPC's ground connection. The MCP2200's USB header must be linked to
a PC's USB connection to allow the terminal program to receive the PIC's ADCC data.

The terminal program should be configured to accept:
            *90909 Baud Rate
            *8-bit data
            *No Parity
            *1 Stop bit
            *No flow control

Once the PIC has been programmed, the ADCC is placed in Average mode. For this mode, 
the ADCC will sample the ADCC input four times, calculate the average after each sample, and perform a 
threshold test after all four samples have been averaged. This is the default state of the demo.
LEDs D2 and D3 are not illuminated.

Pressing the HPC's S1 button once will reconfigure the ADCC into Burst Average mode.
In Burst Average mode, the ADCC takes four samples consecutively, then calculates the average
after all four samples have been taken (rather than after each sample in Average mode). Threshold testing 
is done after the average has been taken. LED D2 is illuminated in this mode.

Pressing the HPC's S1 button twice will reconfigure the ADCC into Basic mode. In Basic mode,
the ADCC operates as a typical ADC. In other words, the ADCC takes a sample, then performs a
threshold test on that sample. No averaging is done. LED D3 is illuminated in this mode.

Pressing the HPC's S1 button a third time will bring the ADCC into LPF mode. LEDs D2 and D3 are
both illuminated. 

Pressing the HPC's S1 button a fourth time will bring the ADCC into Average mode, and neither
LED D2 or D3 are illuminated. 
