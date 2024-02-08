# Yorick geoffre's portfolio

Hi, my name is Yorick Geoffre and i'm a 4th year embedded enginerring student at UCA (université Clermont Auvergne), currently enrolled in the setsis course (embedded systems for signal processing).   

This document is a portfolio detailing the most interesting projects i have completed over the years, as part of my studies or hobbies.

### note
you may see that a lot of my board are branded as being manufactured by "Taipan Labs", that is my maker name online, the boards were still all created by me.

## Table
- esp-wake, the simple iot alarm clock
- kamlibri, the compact usb camera platform
- piconaut, a microcontroller platform dedicated to AR/VR projects
- XRHS, an extended reality framework for linux
- OS.LL, an arm based linux laptop
- minimagick, an extremely cost-optimised IMU-based IK capture system for VR
- TScan, a better windows driver for industrial zebra scanners
- Logitron, a powerful logic analyzer based on the RP2040, compatible with sigrok and other standard tools.

### esp-wake
This project started when i finally had enough of my old brandt-brand alarm clock, which had various issues including overly strong lighting, poor sound quality and a general lack of connectivity.   

<img src="./images/espwake/wake1.jpg"/>

It's an esp32-S2 based alarm clock that can connect over wifi to sync with a time server, it also has a web server that can be used to set the various alarms for up to an entire month, and any music can be used as an alarm as long as it is loaded as a .wav file on its microSD card.

<img src="./images/espwake/wake2.jpg"/>

Optionnally, a 0.93 inch oled display can be connected to it's expansion port on the right, which will provide the user with the complete date as well as temperature, humidity, and air quality of the room in TVOC (the air quality changes the time LEDs's colors as well, from green to red to white).

<img src="./images/espwake/wake3.png"/>
<img src="./images/espwake/wake4.png"/>

Internally it has a dedicated low noise supply for the audio circuit which works over I2S using a MAX brand integrated DAC/Amp combo to get a clean and  glitch-less audio signal out, which is something that cheap audio players tend to fail to deliver on.

The micro SD can be used to store the temperature, humidity, light level and air quality data over time as well for metering. This alarm clock even has an accelerometer for detecting when you tap on your bedside table instead of fumbling to find the buttons in the dark to stop the alarm early in the morning...

It is fully open source and can be found completed at the following git repository:

https://github.com/Kanken6174/esp_wake