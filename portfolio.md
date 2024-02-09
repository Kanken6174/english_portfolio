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

Now this board does work, it is a linux based board that's able to capture raw video footage from a wide variety of sensors, it can do picture enhancement as well as AI based feature detection thanks to its NPU, but there is one key element that's missing, the video encoder.   
This means that i'm forced to work with uncompressed RAW10 video, where each 1080p frame is around 6mb, which is wholly unuseable for a usb webcam. The hardware encoder is present on that chip but not in the open source SDK, only the proprietery SDK has it. To access it i would need to contact allwinner as a company and sign an NDA with them, which as an individual i'm not able to do, so i'm SOL on that front for now.

## Piconaut

Picontaut is a microcontroller board that is specifically meant to be used in AR/VR projects that need a fast MCU while staying fairly compact and cheap. It is based on the RP2040 and has:
- a BMI 270 6 axis IMU
- a QMC5833L 3 axis magnetometer
- a full charge and discharge BMS circuit (DW01A/TP4056)
- a highly efficient buck/boost converter circuit for battery power

<img src="https://media.discordapp.net/attachments/733969551137570849/1108500387473920071/IMG_20230517_230419_631.jpg?ex=65d6656f&is=65c3f06f&hm=ec819888c1fcb4c4fc51f6be6a7b2ba7cf44cfeb2e1ab1db045255156a47d2d0&=&format=webp&width=371&height=300"/>

It also has an expansion port on the back in the form of a microSD port, which lets you plug in a microSD card and talk to it over SPI, or connect a wide variety of microSD-shaped wireless modules, the one in the picture above is my ESP32C3-mini based module which has wifi and bluetooth.

<img src="https://media.discordapp.net/attachments/733969551137570849/1108500387863998504/IMG_20230517_230354_853.jpg?ex=65d6656f&is=65c3f06f&hm=b53788293a5c59dd23043916be3e75b89e025b8b8b4edeb65bab9f80e95318b1&=&format=webp&width=371&height=330"/>

The key feature of this mcu is its built in software library that handles all the filtering maths related to the IMU-MAG couple to output a clean eulerian angle, or a single quaternion. This lib also handles manual calibration of the system over a serial text communication.

## XRHS
XRHS, or eXtended Reality Helmet System, is both a hardware and software framework. It's a three-part system:

### the hardware
XRHS's hardware is only meant as a developpement platform for the software side and changes very often. In its current form it is a fully enclosed helmet which embarks an orange pi 5 ARM computer as well as custom optics and 1440x1440 screens, per eye.

<img src="https://media.discordapp.net/attachments/733969551137570849/1164260569960947762/IMG_0772.jpg?ex=65d63926&is=65c3c426&hm=56fadcbbf33f59a7012ded0b66f0ab7a9caf441bad5d99623fc5d944b8bd33e7&=&format=webp&width=495&height=450"/>
<img src="https://media.discordapp.net/attachments/733969551137570849/1160828301854638100/IMG_20231009_083445_512.jpg?ex=65d2f71a&is=65c0821a&hm=8bd8eb951c452be09c5efb7a33b2311dfa5cd4150940742b3ce5f93e628c3b19&=&format=webp&width=660&height=660"/>
note: in the above picture, the dev-link cable is plugged in, which is not usually present when in use (black usb-c cable)

the helmet can do:
- qr code detection and on-screen data display
- Heat vision, using an MLX90640 low res thermal sensor
- eye tracking, using the medusa boards and ir illuminators
- full, low latency video passthrough from the external cameras

The helmet has its own power source, which is an external battery pack you would usually wear on a belt or harness, it is able to output 2x5V at 20W each (one usb-c is for the orange pi 5, the other is for the axuiliary systems such as the screens and cameras):
<img src="https://media.discordapp.net/attachments/733969551137570849/1160987499242467478/IMG_20231009_190927_415.jpg?ex=65d38b5d&is=65c1165d&hm=6fda2fff4be7eeb3be49ff1db6268f8c455fdc9721b6b6a7af02a3e0828be2c2&=&format=webp&width=660&height=660"/>
The power supply has a few smart features, like power metering and remote shutdown, which can be accessed from the 4 pin connector on the right.

the quality of the onboard screens is quite good, giving the user a sharp image devoid of individual pixels, with little deformation or glare, and as a bonus the feild of view is very large, giving a high sense of immersion:

<video controls>
<source src="https://cdn.discordapp.com/attachments/733969551137570849/1142853394197917796/VID_20230820_110530.mp4?ex=65d22c2a&is=65bfb72a&hm=e274e1f97f051c3d8d4b5e38eeca0d05c3a22470566fe1c00dfb005a1b7bed99&"/>
</video>

using a rail attachement system, the optics can be quickly removed and cleaned or maintained. Without the use of any tools.

<img src="https://media.discordapp.net/attachments/733969551137570849/1143256200620806144/IMG_20230821_202414_637.jpg?ex=65d3a34e&is=65c12e4e&hm=7973cd83e1f1fcff27d524b82eebec3daefeb3c96af65e2484d172cf4c851770&=&format=webp&width=660&height=660"/>

The battery system has two parts, a power module and a power cell. Each power cell can power the helmet for around 7-8 hours on light use. They're made with two 10AH lithium-polymer cells in parrallel, giving a final pack value of 20AH at 3.7V, that's a total of 74WH. Accounting for inefficiencies in the system, i measured a total efficiency of 94.7% on average, so 70WH total.   

Given that the orange pi 5 + screens consume around 14.5W on high load (gpu cpu and npu maxed out), you can excpect a full load battery life or around 70/14.5 ~= 4,83 hours or 4 hours and 49.8 minutes.   

Since the power cells can be swapped out, two of them could get you through a pretty intense day of use.   

<img src="https://media.discordapp.net/attachments/733969551137570849/1167794604091904041/IMG_20231028_135839_133.jpg?ex=65d09f7a&is=65be2a7a&hm=1ce1ab72961c37c7607bd4c5bcbdf2d64c514bc5326cf7c750202736cd233d99&=&format=webp&width=371&height=500"/>

The prcoessor of the orange pi 5, the onboard computer, is the RK3588S from rockchip, it is an 8 core, 2.2ghz cpu with a very powerful gpu for this class of SOC.

<img src="https://media.discordapp.net/attachments/733969551137570849/1144362627791855616/IMG_20230824_220822_865.jpg?ex=65d7a9bf&is=65c534bf&hm=670dc24f3577fd00aa2ed57e7671c2fa997afab6cbb86b72b70bcf5c31241d03&=&format=webp&width=660&height=660"/>

As you can see on this picture, when it is running the xrhs software the onboard computer only takes in about 9.5W, which is what you can excpect for most use cases. That means a total power draw of around 12W, which boosts the battery life to 5.8h hours.