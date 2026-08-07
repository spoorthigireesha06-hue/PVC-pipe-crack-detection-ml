# Hardware Design
## Transmitter Circuit(designed)
- due to failure of power supply, Implemented for first 100 samples collection only
- replaced this circuit directly with nebulizer piezo for transmission
 - ESP32 GPIO → MCP1407 gate driver → IRF530N MOSFET → Piezo
- Driven at 108-110kHz via LEDC PWM
- 12V supply for gate driver
- <img width="1280" height="825" alt="image" src="https://github.com/user-attachments/assets/71c45d52-0ae9-48b5-befc-6f53ba4abb6c" />


## Receiver Circuit
- Piezo RX → NE5534 op-amp (non-inverting amplifier)
- Gain: 47x (Rf=47kΩ, Rin=1kΩ)
- Output → STM32 PA0 (ADC1_IN0)
- <img width="1124" height="1280" alt="image" src="https://github.com/user-attachments/assets/61e13d4a-9e39-4f1e-a970-708820c7845e" />


## Signal Processing
- ADC: 500kHz sampling, 12-bit resolution
- DMA: Circular mode, TIM2 TRGO trigger
- FFT: 1024-point CMSIS-DSP real FFT
  

