# Using the PIC18F26K42's ADC with Computation Module (ADCC)

## Objective:

The ADC with Computation module is a 12-bit ADC that integrates computational functions into module hardware. In this code example, the user can select from four computation modes:

-     Basic mode
- Average mode
- Burst-Average mode
- Low-Pass Filter mode

Basic mode is considered a ‘legacy’ mode since it does not use the computation functions, similar to a typical ADC found in many PIC16 and PIC18 devices. Average mode computes the average of a user selectable number of samples. Burst-Average mode also computes the average of a user selectable number of samples, but acquires the total number of samples without resetting the GO bit between each sample. Low-Pass Filter mode removes unwanted frequencies from a signal.

<div>
  <style>
    div {
      background-color: darkgray;
    }
    span {
      color: #f00;
    }
  </style>
  <span>Im red</span>
</div>

## Demo Configuration:

The Curiosity High Pin Count (HPC) Development Board (DM164136) is used as the test platform. The HPC board has a potentiometer that is connected to an analog input (RA0), which is used for Basic, Average, and Burst-Average modes. Switch S1 is used to select the ADCC mode, and LEDs D2 and D3 are used to determine which mode is active. For Low-Pass Filter mode, a function generator is connected to an analog input (RA1). In Basic, Average, and Burst-Average modes, the ADCC’s conversion results are transmitted to a PC terminal program for viewing over the UART using the MCP2200 USB-to-UART Breakout Module (ADM00393) with the UART TX output connected to pin RC6.

### Curiosity HPC with MCP2200 Breakout Module:

![](https://static.transim.com/img/52018/5a411f3921b1452eaf5a9c97f9928980-7l7d1.jpg){width=auto height=auto align=center}

## ADCC Configuration:

The ADCC configuration can be found in the adcc.c file located in the project folder. Upon power-up, the demo defaults to Average mode, which calls the initialization routine configured for Average mode. In Average mode, both LED D2 and D3 are off. When S1 is pressed once, the software selects Burst-Average mode, the configuration for Burst-Average mode is loaded, and LED D2 is illuminated. When S1 is pressed a second time, software selects Basic mode, the configuration for Basic mode is loaded, LED D2 is turned off, and LED D3 illuminates. When S1 is pressed for the third time, software selects Low-Pass Filter mode, the configuration for Low-Pass Filter mode is loaded, and both LED D2 and D3 are illuminated. If S1 is pressed a fourth time, the program loads the default Average mode, and the mode selection cycle begins again.

### ADCC Mode Selection Code Snippet:

![](https://static.transim.com/img/52018/1ad3fefd3018456ba6e1e057b32057dd-4zxns.jpg){width=auto height=auto align=center}

## UART Configuration:

The UART is configured with an odd baud rate of 90, 909 bps. This is due to the Low-Pass Filter mode timing requirements. When selecting a PC terminal program for data viewing, the serial port should be configured as follows:

### UART/Serial Port Configuration:

![](https://static.transim.com/img/52018/6cfb57bebcf64c8bbe34b2c4203b3a49-t16t0.png){width=auto height=auto align=center}

## Demo Operation:

For Basic, Average, and Burst-Average modes, a user-defined setpoint is compared to the conversion result. The difference, or error, is compared to an upper and lower user-defined threshold, and if the error is within the threshold boundaries, the ADRES value is displayed. If the error is out of the threshold boundaries, the threshold that was violated is displayed. In Basic mode, no threshold testing is performed, and only the current ADRES value is displayed. For these three modes, the potentiometer is used as the ADC input. Turning the potentiometer to the left or right changes the potentiometer’s resistance, which changes the input voltage to the ADCC. The ADRES values in these modes represent the input voltage received from the pot.

### PC Terminal Display When ADRES Value is Within Threshold Limits:

![](https://static.transim.com/img/52018/565d032519314e4fad56813e63eae568-9n74z.png){width=auto height=auto align=center}

### PC Terminal Display When ADRES Value is Violates Upper Threshold Limits:

![](https://static.transim.com/img/52018/66e23d8755f84f62b21b1ece0c9f9534-ds7nm.png){width=auto height=auto align=center}

### PC Terminal Display When ADRES Value is Violates Lower Threshold Limits:

![](https://static.transim.com/img/52018/c5cfd273f72147aeb1d98f0a7b8484f7-ndtcp.png){width=auto height=auto align=center}

### PC Terminal Display in Basic Mode:

![](https://static.transim.com/img/52018/bddc386599de407eaaf1cf5079617ce2-0yb77.png){width=auto height=auto align=center}

For Low-Pass Filter mode, a function generator is connected to the RA1 input pin. The function generator is configured so that a 50 Hz sinewave, with a peak-to-peak voltage of 2V, offset by 1500 mV (since the ADC cannot read values below the negative reference), is fed into the analog input. After each sample, the ADFLTR result is transmitted to the Atmel Studio IDE over the UART. Atmel Studio contains the Data Visualizer plug-in tool that has the ability to decode and display the UART data in the form of a graph, oscilloscope, or a terminal window. For this example, the oscilloscope is used to display the decoded waveform data.
The Data Visualizer should be configured such that the serial port’s baud rate, parity settings, and Stop bit information matches the UART settings. Additionally, the Data Visualizer requires a configuration file that is used to decode the incoming data stream. This text file is included in the example code project file, and is named “Data Stream Config File”.
>Once the Data Visualizer is configured and the Low-Pass Filter mode is running on the HPC board, the filtered waveform will appear on the Data Visualizer’s oscilloscope. When the sinewave’s frequency is increased and reaches approximately 270 Hz (-3dB roll-off frequency), the waveform will have reduced its peak-to-peak voltage range to approximately 70% of the original waveform’s peak-to-peak range. As the frequency continues to increase, the waveform will continue to shrink until it approaches the Nyquist limit.

### Data Visualizer Oscilloscope Displaying the Filtered 50 Hz Sinewave:

![](https://static.transim.com/img/52018/4eef31112f6b4c9da9a16dabd84b607d-n98xs.png){width=auto height=auto align=center}

### Data Visualizer Oscilloscope Displaying the Filtered 270 Hz Sinewave:

![](https://static.transim.com/img/52018/564c89e5d0c94920b83763089ce57e62-22xwk.png){width=auto height=auto align=center}

## Conclusion:

The ADCC with Computation module is used to convert an analog signal into a binary representation of the signal. This code example highlights the use of Basic, Average, Burst-Average, and Low-Pass Filter modes. For more information on the ADCC, please refer to the PIC18F26K42 data sheet.

<div>
      <html>
        <head>
          <style>
            div {
              background-color: darkgray;
            }
            span {
              color: #f00;
            }
          </style>
        </head>
        <body>
          any
        </body>
      </html>
      <span>Im red</span>
    </div>

# proper picture tag
<picture>
    <source media="(prefers-color-scheme: light)" srcset="images/flow-light.png">
    <source media="(prefers-color-scheme: dark)" srcset="images/flow-dark.png">
    <img alt="Shows a flowchart of the software's architecture." src="images/flow-light.png"  width="1000">
</picture>

# Improper picture tag
<picture>
    <source media="(prefers-color-scheme: light)" srcset="images/flow-light.png">
    <source media="(prefers-color-scheme: dark)" srcset="images/flow-dark.png">
</picture>

<center>

| Board | Switch name |  OFFERING TYPE | 
| -----: | :-----------: |  :--- |
[PIC32MZ Embedded Graphics with Stacked DRAM (DA) Starter Kit (Crypto)](https://www.microchip.com/DevelopmentTools/ProductDetails/DM320010-C) | SW1 | MCU |
| hello | World |  MCU |

</center>

| Board | Switch name |  OFFERING TYPE | 
| -----: | :-----------: |  :--- |
[PIC32MZ Embedded Graphics with Stacked DRAM (DA) Starter Kit (Crypto)](https://www.microchip.com/DevelopmentTools/ProductDetails/DM320010-C) | SW1 | MCU |
| hello | World |  MCU |

<div style="display: flex; justify-content: right;">

| Board | Switch name |  OFFERING TYPE | 
| -----: | :-----------: |  :--- |
[PIC32MZ Embedded Graphics with Stacked DRAM (DA) Starter Kit (Crypto)](https://www.microchip.com/DevelopmentTools/ProductDetails/DM320010-C) | SW1 | MCU |
| hello | World |  MCU |
</div>

[//]: <> (This is also a comment.)

[//]: # (This may be the most platform independent comment)

 <!-- A comment line to see how this text is getting handled>
 </!-->
 ✅

# (This is a comment)

# "And this is a comment"

# 'Also this is a comment'

# (Yet another comment)

# (Still another comment)
