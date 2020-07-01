# How-to-Write-GPIO-in-Cube-HAL

Tweaking HAL SPL Library		June 30, 2020

I chose to test the CubeL1 HAL standard library to get the gpio LEDs blinking on my 
STM32L1 Discovery board. It confirmed that it is a "One Size Fits All" meaning the
library is enormous or "bloated" as others would describe. I managed to trim it down by
copying only the relevant directory files but it was still a lot of code considering I
was only going to just blink two LEDs. Instead of tweaking the include paths so the
compiler will find my files and any libraries, I just copy and maintained the same 
directory structure. Take a cue from "Options for Target".

C/C++ Tab

Preprocessor Symbols:

Define: USE_HAL_DRIVER,STM32L152xC,USE_STM32L152C_DISCO

Include Paths: ..\Inc;..\..\..\..\..\..\Drivers\CMSIS\Device\ST\STM32L1xx\Include;..\..\..\..\..\..\Drivers\STM32L1xx_HAL_Driver\Inc;..\..\..\..\..\..\Drivers\BSP\STM32L152C-Discovery

Misc Controls: -C99

Compiler control string: -c --cpu Cortex-M3 -D__EVAL -D__MICROLIB -g -O3 --apcs=interwork --split_sections -I ../Inc -I ../../../../../../Drivers/CMSIS/Device/ST/STM32L1xx/Include -I 

By cursory inspection, the HAL SPL v1.4.0 looks similar to STM32 SPL v1.3.1. I hope as I
dive deeper, the defines, data structure, and functions are similar so code rewrite
wouldn't be too much. I see that it still uses GPIO_InitTypeDef struct.

The stm32l1xx.h I noticed are different from each library version, so caveat. Earlier, I 
also compiled stm32l1xx_gpio.c and the remaining c files ok but during linking time, I
stumbled into the assert errors. "Not enough symbols..." you know. I used #define NDEBUG
to no avail.

Anyways, time to study and write newer code based on HAL instead of SPL.

Happy coding!
