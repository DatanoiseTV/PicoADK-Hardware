
## Install the Arduino Pico support

This step is necessary for now, because the PicoADK support is not yet packaged in a release.

```bash
mkdir -p ~/Arduino/hardware/pico
git clone https://github.com/earlephilhower/arduino-pico.git ~/Arduino/hardware/pico/rp2040
cd ~/Arduino/hardware/pico/rp2040
git submodule update --init
cd pico-sdk
git submodule update --init
cd ../tools
python3 ./get.py
```

## Start Arduino IDE and select the board

![image](https://user-images.githubusercontent.com/6614616/202922012-ed16922f-f353-42dd-bd7d-925e63ae62e7.png)

Make sure that a CPU frequency of 133MHz might not be sufficient, so try higher clock speeds like 225MHz.

## Code example

This example will play a 220Hz Square Wave
```cpp

#include <I2S.h>

// Create the I2S port using a PIO state machine
I2S i2s(OUTPUT);

// GPIO pin numbers
#define pMute 25
#define pDemp 23

const int frequency = 220; // frequency of square wave in Hz
const int amplitude = 500; // amplitude of square wave
const int sampleRate = 48000;

const int halfWavelength = (sampleRate / frequency); // half wavelength of square wave

int16_t sample = amplitude; // current sample value
int count = 0;

void setup() {
  pinMode(PIN_LED0, OUTPUT);
  digitalWrite(PIN_LED0, 1);

  pinMode(pMute, OUTPUT);
  digitalWrite(pMute, HIGH); // unmute codec

  pinMode(pDemp, OUTPUT);
  digitalWrite(pDemp, LOW);

  Serial.begin(115200);

  Serial.println("I2S simple tone");

  i2s.setBCLK(PIN_I2S_BCLK);
  i2s.setDATA(PIN_I2S_DOUT);
  i2s.setBitsPerSample(16);

  // start I2S at the sample rate with 16-bits per sample
  if (!i2s.begin(sampleRate)) {
    Serial.println("Failed to initialize I2S!");
    while (1); // do nothing
  }

}

void loop() {
  if (count % halfWavelength == 0) {
    // invert the sample every half wavelength count multiple to generate square wave
    sample = -1 * sample;
  }

  // write the same sample twice, once for left and once for the right channel
  i2s.write(sample);
  i2s.write(sample);

  // increment the counter for the next sample
  count++;

  if(count % 1024 == 0) Serial.println(count);
}
```
