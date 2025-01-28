# RaspberryPi5IntroWorkshop

Welcome to this **RaspberryPi5 Introduction Workshop**! This workshop is designed to provide step-by-step guidance on getting started with Raspberry Pi 5, focusing on GPIO, audio playback, and analog-to-digital conversion (ADC) using the Raspberry Pi.

![image](https://github.com/user-attachments/assets/79804b7c-341f-4457-ad35-ac882b799c8c)

---

## 🚀 Getting Started

### Step 1: Setting Up Your Raspberry Pi 5
1. Ensure you have the following items:
   - Raspberry Pi 5 board
   - MicroSD card (16GB or larger, with Raspberry Pi OS pre-installed)
   - Power supply (USB-C)
   - HDMI cable and monitor
   - Keyboard and mouse
2. Insert the MicroSD card into the Raspberry Pi.
3. Connect the monitor, keyboard, and mouse to the Raspberry Pi.
4. Power on the Raspberry Pi by connecting the power supply.
5. Follow the on-screen instructions to complete the initial setup.

---

## 🌿 Module 1: Working with GPIO Pins

### Example 1: Turning On an LED
1. Build the circuit:
   - Connect the positive lead of the LED to pin 11 via a 1kΩ resistor.
   - Connect the ground leg of the LED to a ground pin.
2. Write the Python script:
   ```python
   import RPi.GPIO as GPIO

   GPIO.setmode(GPIO.BOARD)
   led = 11
   GPIO.setup(led, GPIO.OUT)
   GPIO.output(led, True)
   ```
3. Run the script:
   ```bash
   python3 LED.py
   ```

### Example 2: Blinking an LED
1. Modify the script to blink the LED:
   ```python
   import RPi.GPIO as GPIO
   import time

   GPIO.setmode(GPIO.BOARD)
   led = 11
   GPIO.setup(led, GPIO.OUT)

   blinkNum = int(input('How many times do you want to blink? '))

   for i in range(blinkNum):
       GPIO.output(led, True)
       time.sleep(1)
       GPIO.output(led, False)
       time.sleep(1)

   GPIO.cleanup()
   ```
2. Run the script and specify the blink count:
   ```bash
   python3 blink.py
   ```

---

## 🎵 Module 2: Audio Playback with Raspberry Pi

### Setup Audio
1. Install required packages:
   ```bash
   sudo apt-get update
   sudo apt-get install alsa-utils mpg123
   ```
2. Configure audio output to the headphone jack:
   ```bash
   sudo raspi-config
   ```
   - Go to "Advanced Options > Audio > Force 3.5mm Jack".

### Play an MP3 File
1. Create a Python script to play audio:
   ```python
   import os
   from time import sleep

   song = 'mpg123 -q name.mp3 &'  # Replace 'name.mp3' with the file name
   os.system(song)
   sleep(10)  # Play for 10 seconds
   os.system('pkill mpg123')
   ```
2. Place your MP3 file in the same directory as the script and run it:
   ```bash
   python3 play_audio.py
   ```

---

## 🧪 Module 3: Analog-to-Digital Conversion (ADC)

### Using Arduino for ADC
1. Connect an Arduino to the Raspberry Pi via USB.
2. Install the necessary Python library:
   ```bash
   sudo apt-get install python-serial
   ```
3. Upload the following sketch to your Arduino:
   ```cpp
   int sensor = A0;

   void setup() {
       pinMode(sensor, INPUT);
       Serial.begin(9600);
   }

   void loop() {
       Serial.println(analogRead(sensor));
       delay(200);
   }
   ```
4. Write a Python script to read data from the Arduino:
   ```python
   import serial

   arduinoData = serial.Serial('/dev/ttyACM0', 9600)

   while True:
       if arduinoData.inWaiting() > 0:
           data = arduinoData.readline()
           print(int(data.strip()))
   ```

---

## 🔧 Additional Commands

### Check Raspberry Pi OS Version
```bash
cat /etc/os-release
```

### Update Your System
```bash
sudo apt update && sudo apt upgrade -y
```

### Monitor CPU Temperature
```bash
vcgencmd measure_temp
```

---

## 📚 Resources

- [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/)
- [Raspberry Pi GPIO Pinout](https://pinout.xyz/)
- [Luma LED Matrix Library](https://github.com/rm-hull/luma.led_matrix)

---

Feel free to copy and paste the commands and code snippets above into your terminal or editor to follow along. Happy tinkering with Raspberry Pi 5! 🤖
