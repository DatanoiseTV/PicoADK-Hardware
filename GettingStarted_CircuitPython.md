# Beta support

[Micropython Beta Build for PicoADK (UF2)](https://cloud.datanoise.org/s/bRjAR5mWHggxYKA)

Enter the PicoADK Bootloader Mode by pressing and holding the BOOT button and quickly pressing the RESET button, then releasing
both buttons. Drag and Drop the UF2 file onto the virtual disk which has appeared.

# Example code

Place a small file called fanfare_test-44khz.wav on the virtual disk.

```python
import audiobusio
import audiocore
import digitalio
import board
import array
import time
import math

SAMPLERATE = 8000

f = open("fanfare_test-44khz.wav", "rb")
wav = audiocore.WaveFile(f)

# Generate one period of sine wave.
length = SAMPLERATE // 440
sine_wave = array.array("H", [0] * length)
for i in range(length):
    sine_wave[i] = int(math.sin(math.pi * 2 * i / length) * (2 ** 15) + 2 ** 15)

# Unmute DAC
xsmt_pin = digitalio.DigitalInOut(board.I2S_XSMT)
xsmt_pin.direction = digitalio.Direction.OUTPUT
xsmt_pin.value = True

#sine_wave = audiocore.RawSample(sine_wave, sample_rate=SAMPLERATE)
i2s = audiobusio.I2SOut(board.I2S_BCLK, board.I2S_LRCLK, board.I2S_DOUT)
#i2s.play(sine_wave, loop=True)

i2s.play(wav, loop=True)

time.sleep(10)
i2s.stop() 

```
