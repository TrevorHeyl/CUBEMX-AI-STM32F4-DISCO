# CUBEMX-AI Demo on STM32F4 Discovery

I wanted to see how the performance of a pre=trained HAR-CNN would look on my SMT32F4 disco SDK just because its the only one I had that had enough resources to run the HAR model from ST's demo.

This project is based on the STM32 CUBEMX-AI tutorial found  [here](https://www.youtube.com/watch?v=grgNXdkmzzQ&list=PLnMKNibPkDnG9IC5Nl9vJg1CKMAO1kODW&index=7&t=0s)

It uses the pre-trained Keras (TensorFlow) model found [here](https://github.com/Shahnawax/HAR-CNN-Keras/blob/master/model.h5)
the project is set up on USART3, this SDK does not have an RS232 transceiver or Virtual COM port, so I added a USB/TTL dongle for that.

**My Dev environment is:**
* Windows 7
* STM32CUBEIDE Version 1.0.1
* STM32CubeMX Version 5.2.1
* X-CUBE-AI 3.4.0
* STM32CUBE HAL FW_F4_V1.24.1

Note: The STM32IDE does not correctly add all the required paths, for this project I had to manually add these paths in the C/C++ Paths and symbols of the Project settings, I decided to use the paths to the project files and not the STM32 Install location in order to make this porject more portable:

* C:\Users\...\STM32CubeIDE\workspace_1.0.0\AI_STM32F4DISCO\Drivers\CMSIS\DSP\Include
* C:\Users\...\STM32CubeIDE\workspace_1.0.0\AI_STM32F4DISCO\Middlewares\ST\AI\AI\data
* C:\Users\...\STM32CubeIDE\workspace_1.0.0\AI_STM32F4DISCO\Middlewares\ST\AI\AI\include
* C:\Users\...\STM32CubeIDE\workspace_1.0.0\AI_STM32F4DISCO\Middlewares\ST\Application\Validation\Inc

For interest , here is the build **sizes** for my version:

arm-none-eabi-objdump -h -S  AI_STM32F4DISCO.elf  > "AI_STM32F4DISCO.list"

text	   data	    bss	    dec	    hex	filename

874084	   1680	  59008	 934772	  e4374	AI_STM32F4DISCO.elf
 
 **Performance:** Dismal ;-)











