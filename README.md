# Ultrasonic Distance Measurement System (STM32F4 Embedded Project)

## Overview
This project implements an ultrasonic distance measurement system using the STM32F4 microcontroller and Keil uVision. An ultrasonic sensor (such as the HC-SR04) is interfaced with the microcontroller to measure distances by calculating the echo pulse width. The measured distance is then transmitted via USART3 to a serial terminal for real-time monitoring.

## Features
- **Ultrasonic Sensing:**  
  Measures distance in centimeters by calculating the time between sending a trigger pulse and receiving the echo.
  
- **Timer-Based Delays:**  
  Utilizes TIM2 to generate precise microsecond and millisecond delays necessary for accurate sensor readings.
  
- **USART Communication:**  
  Configures USART3 to transmit distance measurements serially, ensuring reliable single-byte transmission by waiting for the TXE flag to set before sending each byte.

- **Low-Level Hardware Control:**  
  Demonstrates skills in GPIO configuration, timer setup, and peripheral initialization on an STM32F4 microcontroller.

## Hardware Requirements
- STM32F4 Discovery Board or a compatible STM32F4 microcontroller board.
- Ultrasonic Sensor (e.g., HC-SR04).
- Jumper wires and breadboard for circuit connections.
- USB-to-Serial adapter (if required) to view the USART output on a PC.

## Software Requirements
- **IDE:** Keil uVision
- **Compiler:** ARM Cortex-M Compiler (Keil ARM Compiler or equivalent)
- **Libraries:** STM32F4 Standard Peripheral Library (if used)

## Circuit Connections
- **Ultrasonic Sensor:**
  - **Trigger (PC6):** Connect to the sensor's trigger pin.
  - **Echo (PC7):** Connect to the sensor's echo pin.
  
- **USART3 Interface:**
  - **TX (PD8):** Connect to the serial adapter’s RX pin.
  - **RX (PD9):** Connect to the serial adapter’s TX pin.

Ensure that all GPIO pins are correctly configured in both the hardware setup and within the code.

## Code Overview
- **USART3 Initialization:**  
  The `USART3_Init()` function sets up USART3 with a baud rate of 9600. PD8 and PD9 are configured as alternate function pins for transmitting and receiving data.
  
- **Timer Initialization:**  
  `TIM2_Init()` configures TIM2 to run at 1 MHz, enabling microsecond-accurate delay generation.
  
- **Ultrasonic Measurement:**  
  The `measure_distance()` function generates a 10 µs trigger pulse on PC6, then measures the duration of the echo pulse on PC7 using TIM2. The pulse width is converted to a distance in centimeters.
  
- **Data Transmission:**  
  The `USART3_Transmit()` function writes each character of the distance message to the USART Data Register. Writing to this register clears the TXE (Transmit Data Register Empty) flag, ensuring proper sequential transmission.

- **Main Loop:**  
  Continuously measures distance and sends the result over USART3 every 500 ms.

## Building and Flashing Instructions
1. **Open the Project:**  
   Open the project in Keil uVision.
   
2. **Configure the Project:**  
   - Select the appropriate STM32F4 device.
   - Set the compiler options and include necessary libraries.
   
3. **Build the Project:**  
   Compile the project to generate the executable firmware.
   
4. **Flash the Firmware:**  
   Use your preferred flashing tool (e.g., ST-Link Utility) to program the firmware onto your STM32F4 board.
   
5. **Run and Monitor:**  
   Open a serial terminal (set to 9600 baud) to view the distance measurements output by the microcontroller.

