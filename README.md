# PicoDSP

## Introduction

![IMG_1211](https://user-images.githubusercontent.com/6614616/178321463-fd28d750-6690-4bcf-9f1c-f8ad699bd965.jpg)
![signal-2022-07-11-171353](https://user-images.githubusercontent.com/6614616/178331952-df65a58a-e0cd-4261-8613-d4b20d6482e4.jpeg)
![FXZJiSXWAAQjR3J](https://user-images.githubusercontent.com/6614616/178937038-563c2f2a-2c2c-427a-8e2e-35cb2d0831c8.jpeg)

The PicoDSP is a Raspberry Pi RP2040 based Audio DSP Board. It has the same form factor like the Raspberry Pico, but has an additional PCM5102 32-bit I2S Audio Codec.

## Features
* RP2040 Dual Core 133MHz Cortex M0+ (running at 2x 400MHz Overclocked in the RTOS Template)
* 2MB Flash (plenty for synthesizers based on Vult)
* PCM5102 32-bit Audio Codec
* SWD Debug Port
* Pin-compatible with RP2040 besides a few pins

## Software

You can find software examples at https://github.com/DatanoiseTV/RP2040-DSP-FreeRTOS-Template

This template contains the I2S codec drivers, A custom build step for Vult DSP based projects and a synthesizer as an example and should be a good starting point for most projects.

## Future work
* Add castellated holes
* Evaluate increasing flash size
* Add SPI ADC

# Pinout

![pinout](https://user-images.githubusercontent.com/6614616/178937016-82d58e8c-4b84-41af-94fe-c01936c81884.jpeg)

The XSMT signal is the soft mute for the audio codec and the DEMP signal is controling the de-emphasis at 44100 kHz.
Note that there is no FMT pin, as the codec is set to operare in I2S mode.

# First Flashing / Getting started

If you initially get the PicoDSP, you will need to flash your firmware and make sure you include **pico_bootsel_via_double_reset** in the target_link_libraries( ... ) in the CMakeLists.txt and bridge the **BOOT** and **GND** pins, then connect USB and flash the firmware

After that, you can remove the bridge and you will be able to boot into the USB disk mode by fast **double pressing** reset.
