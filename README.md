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

Note: The STM32IDE does not correctly add all the required paths, for this project I had to manually add these paths in the C/C++ Paths and symbols of the Project settings, I decided to use the paths to the project files and not the STM32 Install location in order to make this porject more portable, in case you have build problems, just re-point these paths as the IDE does not add these as relative paths:

* C:\Users\...\STM32CubeIDE\workspace_1.0.0\AI_STM32F4DISCO\Drivers\CMSIS\DSP\Include
* C:\Users\...\STM32CubeIDE\workspace_1.0.0\AI_STM32F4DISCO\Middlewares\ST\AI\AI\data
* C:\Users\...\STM32CubeIDE\workspace_1.0.0\AI_STM32F4DISCO\Middlewares\ST\AI\AI\include
* C:\Users\...\STM32CubeIDE\workspace_1.0.0\AI_STM32F4DISCO\Middlewares\ST\Application\Validation\Inc

For interest , here is the build **sizes** for my version:

arm-none-eabi-objdump -h -S  AI_STM32F4DISCO.elf  > "AI_STM32F4DISCO.list"

text	   data	    bss	    dec	    hex	filename

874084	   1680	  59008	 934772	  e4374	AI_STM32F4DISCO.elf
 
 **Performance:** Dismal ;-)
 
 Here is the Output Log...
 
 C:/Users/Dev/Downloads/model.h5 -t keras_dump --compress 4 --mode stm32 --name network --desc COM4:115200
Matching results...

ON-DEVICE STM32 execution ("network", COM4, 115200)..

<Stm32com id=0xea53c88 - CONNECTED(COM4/115200) devid=0x411/UNKNOW msg=1.0>
 0x411/UNKNOW @168MHz/168MHz (FPU is present) lat=5 ART: PRFTen ICen DCen
 found network(s): ['network']
 description    : 'network' (90, 3, 1)-[7]->(1, 1, 6) macc=874970 rom=775.52KiB ram=44.50KiB
 tools versions : rt=(3, 3, 0) tool=(3, 3, 0)/(1, 1, 0) api=(1, 0, 0) "Sat Jun 22 15:43:25 2019"

Running with inputs=(10, 90, 3, 1)..
....... 1/10
....... 2/10
....... 3/10
....... 4/10
....... 5/10
....... 6/10
....... 7/10
....... 8/10
....... 9/10
....... 10/10
 RUN Stats    : batches=10 dur=2.792s tfx=2.573s 4.190KiB/s (wb=10.547KiB,rb=240B)

Results for 10 inference(s) @168/168MHz (macc:874970)
 duration    : 62.976 ms (average)
 CPU cycles  : 10579924 (average)
 cycles/MACC : 12.09 (average for all layers)

Inspector report (layer by layer)
 signature      : EF7C5473
 n_nodes        : 7
 num_inferences : 10

Clayer  id  desc                          oshape            ms        
--------------------------------------------------------------------------------
0       0   10011/(Merged Conv2d / Pool)  (10, 44, 1, 128)  14.470    
1       4   10005/(Dense)                 (10, 1, 1, 128)   45.291    
2       4   10009/(Nonlinearity)          (10, 1, 1, 128)   0.012     
3       5   10005/(Dense)                 (10, 1, 1, 128)   3.037     
4       5   10009/(Nonlinearity)          (10, 1, 1, 128)   0.012     
5       6   10005/(Dense)                 (10, 1, 1, 6)     0.144     
6       6   10014/(Softmax)               (10, 1, 1, 6)     0.010     
                                                            62.976 (total)


Creating C:\Users\Dev\STM32Cube\Repository\Packs\STMicroelectronics\X-CUBE-AI\3.4.0\Utilities\windows\ai_valid_inputs.csv
Creating C:\Users\Dev\STM32Cube\Repository\Packs\STMicroelectronics\X-CUBE-AI\3.4.0\Utilities\windows\ai_valid_outputs_model.csv
Creating C:\Users\Dev\STM32Cube\Repository\Packs\STMicroelectronics\X-CUBE-AI\3.4.0\Utilities\windows\ai_valid_outputs_c_model.csv


  MACC / frame: 874970
  ROM size:     775.52 KBytes
  RAM size:     44.50 KBytes (Minimum: 44.50 KBytes)
  Comp. factor: 3.722


Validating criteria: L2 relative error < 0.01 on the output tensor

  Ref layer 6 matched with C layer 6, error: 0.0010825497

Validation: OK
 [AI:network]  Validation OK











