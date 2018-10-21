# Debug ATSAMD21G18 (Arduino M0/Zero) with CMSIS-DAP


## Overview
 
Arduino Zero/M0 pro has onboard hardware debugger while Arduino IDE doesn't support debugging when I write this. This tutorial will show you how you can set up debug environment in Visual Studio Code, a cross-platform free IDE with Arduino Plugin.

You can also use a CMSIS-DAP compatible debugger with a customized ATSAMD21G18 board. 

This tutorial is using Mac OS as an example. But I'll explain every detail to help you understand and use it on other platforms.  

## Hardware I used

![set img](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/ArduinoM0_CMSIS.jpg)

I used a customized Arduino M0 board. The SCH and PCB files can be found in this repo. On the right side of this board, there is a 4-pin connector for SWD debugging.

For debugger, I used a DAPlink debugger from jixin.pro. You may get it from [here](https://lcsc.com/product-detail/Others_Jixin-JX160101_C284862.html).

Arduino and debugger are connected with 4 female jumper wires. (3.3V, SWDIO, SWCLK, GND)

