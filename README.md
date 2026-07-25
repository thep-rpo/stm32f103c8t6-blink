# STM32 Bluepill LED Blink

## Description
A simple bare-metal blink project for the STM32F103C8T6 Bluepill board, written in C using STM32CubeIDE and the HAL library. It toggles the onboard LED on pin PC13.

## Hardware Requirements
* **Board:** STM32 Bluepill
* **Programmer:** ST-LINK V2

## Wiring & Pinout
* **PC13:** Onboard Green LED (Note: LED is Active LOW, meaning setting the pin to 0 turns it ON).
* **ST-LINK Connections:**
  * `3.3V`  -> `3.3V`
  * `GND`   -> `GND`
  * `SWDIO` -> `SWDIO`
  * `SWCLK` -> `SWCLK`
  
## Software & Toolchain
* **IDE:** STM32CubeIDE (v2.2.0)
* **Device Configuration:** STM32CubeMX (Integrated into the IDE. Used via the `.ioc` file to configure PC13 as a GPIO Output and generate the initialization code).
* **Debugger:** OpenOCD (Used instead of ST-LINK GDB server to support clone chips).

## Setup Quirks & Flashing
Because of the clone ST-LINK V2 missing the hardware reset line, this project requires a specific OpenOCD configuration to flash successfully:

1. In STM32CubeIDE, go to **Run > Debug Configurations > Debugger**.
2. Set the Debug Probe to **ST-LINK (OpenOCD)**.
3. In the **OpenOCD Options** box, add: `-c "reset_config none"`
4. Move the **BOOT0** jumper to 1.
5. Click **Run** to flash the board.
6. Move the **BOOT0** jumper back to 0.
7. Press the **RESET button** on the board to run the code.
