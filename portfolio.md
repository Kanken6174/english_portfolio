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

## Kamlibri
As i was developping XRHS, i found myself needing to buy more and more costly usb camera modules, on which i had absolutely no control as far as additionnal feautres or picture enhancement went. This is why i took it upon myself to create a compact usb camera system that i could actually build myself, for cheap, and in a sustainable way (that is with parts i know i could obtain in large quantities).

I looked through many different chip vendors before finally finding the one chip that met all my needs, the V851S from allwinner. It is a 4.5€/pc chinese arm A7-based microprocessor with 64mb of ram, which can run linux in headless mode, as well as connecting to various mipi-csi and parrallel-csi cameras. It also has a 1080p60 MJPEG encoder and a native usb 2.0 peripheral.

This device had all the building blocks that i needed in order to create my custom camera, i used it to create this first prototype, which was codenamed "lineye" (linux eye), and was sponsored by the UCA for board fabrication costs:

<img src="https://media.discordapp.net/attachments/733969551137570849/1171156641652154468/IMG_20231106_193808_625.jpg?ex=65d3a01e&is=65c12b1e&hm=fda4dbaadaacd582961e486d01c5c9cfab8299c48a2029e282f28da8f89aee9c&=&format=webp&width=371&height=350"/>

<img src="https://media.discordapp.net/attachments/733969551137570849/1171156642226770013/IMG_20231106_191424_371.jpg?ex=65d3a01e&is=65c12b1e&hm=ccd38c3ce629edfc5491a6d5e1ddf7aa4ef198812fee4cccd3da4ebc8b8b8a78&=&format=webp&width=371&height=330"/>

It was quite capable and was able to acquire its first images using a GC2053 (galaxycore brand) camera sensor:
<img src="https://media.discordapp.net/attachments/785631967529271347/1190675024852566029/image.png?ex=65d0ce07&is=65be5907&hm=11120e56adbf0bbbc07979b113db5839cd00f3d472ece917c37d5292b0496e61&=&format=webp&quality=lossless"/>

The onboard ISP was especially useful to color and lens correct the various images. The one big issue with this design was its size, this was fixed with its next iteration, the kamlibri:

<img src="https://media.discordapp.net/attachments/733969551137570849/1199750695293829240/IMG_20240124_172020_004.jpg?ex=65d622e8&is=65c3ade8&hm=d5773d95f22ea631f72f44ae2d627b552399ff26a201262bebed2aaf8a1ee087&=&format=webp&width=1173&height=660"/>
<img src="https://media.discordapp.net/attachments/733969551137570849/1199751279807836330/IMG_20240124_172306_515.jpg?ex=65d62373&is=65c3ae73&hm=d8be6266cdd5ddad229dab522159a383f520b391c2512e400647c3709d3ab0f3&=&format=webp&width=1173&height=660"/>
