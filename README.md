# PicoADK - Pico Audio Development Kit

# Introducing the PicoADK+
![image](https://user-images.githubusercontent.com/6614616/198906826-37f1ca64-14bd-4d27-a55e-15f008642603.png)

The PicoADK+ (we had to change the name PicoDSP) is a RP2040 based Audio Development Kit, which allows you to build your own digital oscillators, synthesizers, noise boxes and experiment around. It has all the base features of the Raspberry Pico, plus a high quality Audio Output, 8 Analog Inputs for connecting potentiometers, control voltage from eurorack systems or even additional input signals.

# Specifications
* RP2040 Dual Core 133MHz Cortex M0+ (running at 2x 400MHz Overclocked in the RTOS Template)
* 2MB Flash (plenty for synthesizers and sound generators)
* PCM5100A 32-bit Audio Codec
* SWD Debug Port
* Very low noise LDO regulators (separate LDO for digital circuits and separate for analog circuits)
* No switching regulators
* Pin-compatible with RP2040 (besides a few pins internally used or rearranged)
* PCM5100A 32-bit, up to 384KHz I2S Audio Codec
* Dedicated Boot and Reset Buttons
* 8 channel 12-bit ADC with up to 1MS/s, with selectable 3.3V range (on-board low-noise power supply) or range up to 5V via external VREF
* Low-Pass filter on each ADC input (fMax=48 KHz) at low-impedance (100 Ohm). With 5V VREF suitable for CV (no overvoltage protection, unipolar)
* Series resistors on ADC SPI to improve signal integrity and reduce crosstalk
* Symbols marking special pin functions on the pin headers
* 4 LEDs on shared GPIO2-5 for debugging
* GPIO15 is hard-wired to a LED
* ESD Protection on USB

# Pinout (PicoADK+ v1.1) - 48 Pin

![image](https://user-images.githubusercontent.com/6614616/198907086-aaeb9831-ceb2-4acc-8242-45671ba2a3fd.png)

Interactive pinout at https://datanoise.net/picoadk/

New in the PicoADK+ v1.1:
* 8 additional 12-bit ADC Inputs with external separate supply VEXT (up to 5v)
* Solder jumper on the bottom of the PCB for selecting internal 3.3VA ADC supply or external VREF.

The XSMT signal is the soft mute for the audio codec and the DEMP signal is controling the de-emphasis at 44100 kHz.
Note that there is no FMT pin, as the codec is set to operare in I2S mode.

The SPI ADC shares the GPIO10 to GPIO13, which are also present on the pin headers. Please be aware of that.

# First Flashing / Getting started

* Press and Hold the B(OOT) button and press reset quickly. Afterwards release the BOOT button and you will see a RP2_BOOT drive on your computer.

# Caveats (v1 + v1.1)

Make sure your software controls the XSMT and DEMP pins. The XSMT needs to be controled by the software to mute/unmute the audio output.
With the DEMP pin you can control the Deemphasis for 44100 Hz.

## Software

You can find software examples at https://github.com/DatanoiseTV/RP2040-DSP-FreeRTOS-Template (currently some rework in progress, this was for the first "Big PCB" version).

This template contains the I2S codec drivers, A custom build step for Vult DSP based projects and a synthesizer as an example and should be a good starting point for most projects.


# More Pictures (v1, non plus)
![signal-2022-07-11-171353](https://user-images.githubusercontent.com/6614616/178331952-df65a58a-e0cd-4261-8613-d4b20d6482e4.jpeg)
![FXZJiSXWAAQjR3J](https://user-images.githubusercontent.com/6614616/178937038-563c2f2a-2c2c-427a-8e2e-35cb2d0831c8.jpeg)

