
# 6S Li-Ion Analog Battery Level Indicator 🔋

An analog, MCU-free battery level indicator designed specifically for a 6S Lithium-Ion power bank (optimized for cells like the ASPİLSAN INR18650A28). The circuit reads the battery pack's voltage and displays the remaining capacity using four SMD LEDs. 

This project was custom-designed from scratch, including schematic capture and PCB layout.

## 📌 Features
* **Fully Analog Design:** No microcontrollers or code required; purely relies on voltage comparators.
* **Safe Discharge Calibrated:** Specifically tuned for a 20.0V to 24.0V range to maximize the cycle life of 6S Li-Ion packs, preventing deep discharge.
* **Custom Resistor Ladder:** Uses standard components (and some clever series/parallel connections) to achieve precise reference voltages.
* **Low Standby Drain:** Designed to be used with a push-button to ensure zero battery drain when the indicator is not being actively viewed.
* **SMD LED Display:** Clean and compact visual feedback.

## 📊 Voltage Thresholds
The circuit utilizes a voltage divider (47kΩ / 10kΩ) and a custom resistor ladder against a 5.1V Zener diode reference to trigger LM358 Op-Amps at specific voltage levels:

| LED Indicator | Capacity | Trigger Voltage (Pack) | Per-Cell Voltage |
| :--- | :--- | :--- | :--- |
| **LED 4 (Top)** | 100% | > 24.00V | 4.00V |
| **LED 3** | 75% | > 22.67V | ~3.78V |
| **LED 2** | 50% | > 21.33V | ~3.55V |
| **LED 1 (Bottom)** | 25% | > 20.00V | ~3.33V |

*(Note: Below 20.0V, all LEDs turn off, indicating the power bank must be recharged immediately to prevent cell degradation).*

## 🛠️ Hardware & Component Notes
Since the exact calculated resistor values are sometimes hard to source, this PCB incorporates practical engineering workarounds:
* **The Comparators:** 2x LM358 DIP-8 ICs handle the 4 distinct voltage comparisons.
* **Reference Ladder:** Instead of obscure precision resistors, the internal reference steps are achieved using three identical **470Ω** resistors, bracketed by a **1.8kΩ** resistor at the top and an **8.2kΩ** resistor at the bottom.
* **Series/Parallel Workarounds:** Where specific values like 2.2kΩ (1/2W) were needed for LED current limiting and Zener protection but unavailable, standard 1/4W resistors were combined in parallel (e.g., two 4.7kΩ resistors) to achieve the target resistance and double the power dissipation limit.

## 📐 Schematics & PCB Layout
*(Add your schematic and PCB images here by replacing the local paths)*

### Circuit Schematic
![Schematic](images/schematic.png)
<img width="1053" height="521" alt="Ekran görüntüsü 2026-04-30 003648" src="https://github.com/user-attachments/assets/019d69d5-ece4-41e3-9b48-c4bab6c105eb" />

### PCB Layout (2D)
<img width="648" height="604" alt="Ekran görüntüsü 2026-04-30 003640" src="https://github.com/user-attachments/assets/4a7f8516-f11b-4868-bad3-dfa7a758a52f" />
<img width="1053" height="521" alt="Ekran görüntüsü 2026-04-30 003648" src="https://github.com/user-attachments/assets/019d69d5-ece4-41e3-9b48-c4bab6c105eb" />

### 3D Render
<img width="745" height="789" alt="Ekran görüntüsü 2026-04-30 003614" src="https://github.com/user-attachments/assets/9798a90b-dbca-4cb0-9975-740d2a59552e" />

## 🚀 Usage Instructions
1.  **Connection:** Connect the `GND` of the board to the battery pack's negative terminal.
2.  **Push-Button Integration:** Connect the `VCC` of the board to a momentary push-button, and the other side of the button to the battery pack's positive terminal. **Do not connect directly to VCC permanently**, as the Zener diode and voltage dividers will draw a small continuous parasitic current (~10-15mA) and slowly drain the power bank.
3.  **Reading:** Press the button. The number of illuminated SMD LEDs represents the current charge tier.

## 📝 License
This project is open-source. Feel free to use, modify, and integrate this indicator into your own DIY battery and power bank projects.
