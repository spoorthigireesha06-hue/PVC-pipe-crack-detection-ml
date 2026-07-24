# PVC-pipe-crack-detection-ml
Real-time PVC pipe crack detection using 110khz ultrasonic acoustic transmission,STM32F401 FFT signal processing, and ML classification(ANN) across four pipe conditions.
# System architecture
Ultrasonic nebulizer(108-110khz)-> PVC pipe(Test Medium) -> PiezoRX -> NE5534 Op-Amp -> STM32F401 ADC(500kHz) -> 1024-point FFT -> Feature extraction-> ml classification -> Pipe condition output
# Hardware Used
| Component | Role |
| 110kHz Ultrasonic Nebulizer | Acoustic transmitter |
| Piezo transducer | Signal receiver |
| NE5534 Op-Amp | Signal conditioning |
| STM32F401CCUx | ADC + FFT processing |
| ESP32 | Transmitter circuit (designed) |
| MCP1407 + IRLZ44N/IRF530N | Gate driver + MOSFET |
# Four Pipe Conditions
| Condition | Samples |
| Empty Normal | 269 |
| Empty Cracked | 202 |
| Flowing Normal | 229 |
| Flowing Cracked | 329 |
| Total | 1029 |
# ML Pipeline
- Feature extraction from FFT magnitude spectrum
- Stratified 80/10/10 train/val/test split
- SMOTE balancing on training data only
- Three models compared
# Results
| Model | Val Accuracy | Test Accuracy |
| PyTorch Artificial Neural Network | 92-93% | 97% |
| Random Forest | 93.7% | 98% |
| XGBoost | 89% | 98% |
# images
<img width="1200" height="1600" alt="IMG-20260519-WA0012" src="https://github.com/user-attachments/assets/6f0b52fe-2483-4a61-8687-4a48e8a62421" />
<img width="2004" height="1769" alt="confusion_matrix_Multilayer_Perceptron_(MLP)" src="https://github.com/user-attachments/assets/8caab2cc-cbe3-4919-9abe-70cb62c1be6a" />
<img width="1537" height="1023" alt="image" src="https://github.com/user-attachments/assets/1e5778a3-6e8f-4e39-b125-6bc5ede0ff14" />










## Repository Structure
