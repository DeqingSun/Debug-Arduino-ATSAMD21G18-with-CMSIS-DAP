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

First make sure you are using a new version of Arduino. Get a new version of Arduino IDE from [Arduino website](https://www.arduino.cc/en/Main/Software).

Then you need to make sure if you have installed support for Arduino M0. Go to "Tools"->"Board"->"Boards Manager". Find "Arduino SAMD Boards (32-bit ARM Cortex-M0+)", install it.

![upload firmware](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/installboard.png)

Now you will be able to select Arduino M0 Pro board. We select "Arduino M0 Pro (Programming Port)" in "Board" and "Atmel EDBG" in "Programmer". Then we click "Burn Bootloader".

![upload firmware](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/uploadFirmware.png)

If it doesn't work, try to replug USB. Check your soldering and connection if it still doesn't work.

Open "File"->"Examples"->"01.Basics"->"Blink" and upload the code. See if you get LED blinking.

![upload blink](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/arduinoUpload.png)

When you see your LED blinking, that means your Arduino, debugger, connections are all correct.

"Save as" Blink example into a folder. We will use it later.

## Step 2, setup VScode

First download VScode from <https://code.visualstudio.com/>

![download VScode](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/downloadVScode.png)

Enable extensions side bar.

![Enable extensions](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeShowExtensions.png)

Look for Arduino extension (the offical one from Microsoft, not a random person) and install it.

![Install Arduino](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeInstallArduino.png)

Then you install Arduino extension. 

Click reload after you finish install.

![reload Arduino](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeReload.png)

## Step 3, Add support for CMSIS-DAP

Quit Vscode (not close the window)

![reload Arduino](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeQuit.png)

In Mac, open finder, Click "Go"->"Go to Folder"

![gotoFolder](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/gotoFolder.png)

Open extension folder (you can copy & paste):

| OS | Path |
|----|------|
| Windows | %USERPROFILE%\.vscode\extensions |
| macOS   | ~/.vscode/extensions |
| Linux   | ~/.vscode/extensions |

Paste path

![gotoFolder](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/gotoFolderPath.png)

Then you will arrive extension folder

![extension Folder](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/gotoFolderExtension.png)

Go into the Arduino extension folder (```vsciot-vscode.vscode-arduino-0.2.22``` at this moment) -> "misc", you will find a debuggerUsbMapping.json file

![extension Folder](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/debuggerUsbMappingLocation.png)

Replace that file with the [one](https://raw.githubusercontent.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/master/debuggerUsbMapping.json) in this repo.

![extension Folder](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/replaceJson.png)

The reason we do this step is that: the USB Vid/Pid pair of the CMSIS-DAP debugger is not supported yet. Once the [PR](https://github.com/Microsoft/vscode-arduino/pull/634) is megered into release, we can skip this step.


## Step 4, Open sketch and debug

Open VScode again. Click "File"->"Open"

![open command](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeOpen.png)

Open the folder containing the sketch file, not the sketch file itself.

![open Folder](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeOpenFolder.png)

On the bottom blue bar, click <Select Board Type>

![Select Board Type](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/selectBoardType.png)

Set Board to "Arduino M0 Pro (Programming Port)".

![set board](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeSetBoard.png)

Switch to Debug tab, add configuration if you don't have one.

![add config](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeAddConfig.png)

Add breakpoints in code.

![add breakpoints](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeBreakpoint.png)

Start Debugging

![start debugging](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeDebugging.png)

Press the continue button to switch LED

![control debugging](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/vscodeDebugControl.png)

-----
## Troubleshoot

If you stop debugging while code is running, openOCD may still keep running. You will not be able to debug again and you may see this error. 

![openocd Error](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/openOCDerr.png)

The error message doesn't make any sense. Try to type ```pkill openocd``` in terminal to kill running openOCD process.

![kill openocd](https://github.com/DeqingSun/Debug-Arduino-ATSAMD21G18-with-CMSIS-DAP/raw/master/img/killOpenOCD.png)

Then you will be able to debug.

