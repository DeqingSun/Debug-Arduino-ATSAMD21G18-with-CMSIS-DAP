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


## Step 1, get Blink example working

First you need to make sure if you have installed support for Arduino M0. Go to "Tools"->"Board"->"Boards Manager". Find "Arduino SAMD Boards (32-bit ARM Cortex-M0+)", install it.

![upload firmware](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/installboard.png)

Now you will be able to select Arduino M0 Pro board. We select "Arduino M0 Pro (Programming Port)" in "Board" and "Atmel EDBG" in "Programmer". Then we click "Burn Bootloader".

![upload firmware](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/uploadFirmware.png)

If it doesn't work, try to replug USB. Check your soldering and connection if it still doesn't work.

Open "Blink example" and upload the code. See if you get LED blinking.

![upload blink](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/arduinoUpload.png)

When you see your LED blinking, that means your Arduino, debugger, connections are all correct.

"Save as" Blink example into a folder. We will use it later.

## Step 2, setup VScode

First download VScode from <https://code.visualstudio.com/>

![download VScode](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/downloadVScode.png)

Enable extensions side bar.

![Enable extensions](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeShowExtensions.png)

Look for Arduino extension and install it.

![Install Arduino](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeInstallArduino.png)

Then you install Arduino extension. 

Click reload after you finish install.

![reload Arduino](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeReload.png)

