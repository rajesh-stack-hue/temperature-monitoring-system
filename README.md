# Temperature Monitoring System 🌡️

## Arduino UNO + LM35 + 16×2 I2C LCD

This project is a simple embedded **Temperature Monitoring System** using an **Arduino UNO**, **LM35 temperature sensor**, and **16×2 I2C LCD**.

The LM35 measures temperature and provides an analog voltage to the Arduino UNO through analog pin **A0**. The Arduino processes the sensor value, displays the temperature on the LCD, and sends the readings to the Serial Monitor at **9600 baud**.

## 🎯 Objectives

* Measure temperature using the LM35 sensor.
* Process the sensor signal using Arduino UNO.
* Display live temperature on a 16×2 I2C LCD.
* Send temperature readings to the Serial Monitor.
* Demonstrate a sensor → controller → display → logging workflow.

## 🛠️ Components Required

| Component               |    Quantity |
| ----------------------- | ----------: |
| Arduino UNO             |           1 |
| LM35 Temperature Sensor |           1 |
| 16×2 I2C LCD            |           1 |
| Breadboard              |           1 |
| Jumper Wires            | As required |
| USB Cable               |           1 |

## 🔌 Circuit Connections

| Device  | Pin | Arduino UNO |
| ------- | --- | ----------- |
| LM35    | VCC | 5V          |
| LM35    | OUT | A0          |
| LM35    | GND | GND         |
| I2C LCD | VCC | 5V          |
| I2C LCD | GND | GND         |
| I2C LCD | SDA | A4 / SDA    |
| I2C LCD | SCL | A5 / SCL    |

> **Note:** LM35 sensor packages can have different physical pin arrangements. Verify the VCC, OUT, and GND pins from the sensor datasheet before powering the circuit.

## ⚙️ Working Principle

1. The LM35 senses the surrounding temperature.
2. It produces an analog output voltage proportional to temperature.
3. Arduino UNO reads the analog signal through **A0**.
4. The Arduino converts the ADC value into voltage and temperature.
5. The calculated temperature is displayed on the **16×2 I2C LCD**.
6. The same temperature reading is sent to the **Serial Monitor** every second at **9600 baud**.

## 💻 Software Requirements

* Arduino IDE
* Arduino UNO board
* LiquidCrystal_I2C library

## 📚 Arduino Program

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

const int TEMP_PIN = A0;

void setup() {
  Serial.begin(9600);

  lcd.init();
  lcd.backlight();

  lcd.setCursor(0, 0);
  lcd.print("Temperature:");

  lcd.setCursor(0, 1);
  lcd.print("Starting...");

  delay(1000);
  lcd.clear();
}

void loop() {
  int rawValue = analogRead(TEMP_PIN);

  float voltage = rawValue * (5.0 / 1023.0);
  float temperatureC = voltage * 100.0;

  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(temperatureC, 1);
  lcd.write((byte)223);
  lcd.print("C ");

  lcd.setCursor(0, 1);
  lcd.print("Raw: ");
  lcd.print(rawValue);
  lcd.print(" ");

  Serial.print("Temperature: ");
  Serial.print(temperatureC, 1);
  Serial.print(" C | ADC: ");
  Serial.println(rawValue);

  delay(1000);
}
```

## 🖥️ Expected LCD Output

```text
Temp: 27.4°C
Raw: 560
```

## 📟 Expected Serial Monitor Output

```text
Temperature: 27.4 C | ADC: 560
Temperature: 27.5 C | ADC: 562
Temperature: 27.5 C | ADC: 561
```

## 🚀 How to Upload

1. Open **Arduino IDE**.
2. Connect Arduino UNO using USB.
3. Install the **LiquidCrystal_I2C** library.
4. Select **Tools → Board → Arduino UNO**.
5. Select the correct **COM Port**.
6. Paste the Arduino program.
7. Click **Verify**.
8. Click **Upload**.
9. Open **Serial Monitor**.
10. Set the baud rate to **9600**.
11. Observe the temperature on the LCD and Serial Monitor.

## 🔧 Troubleshooting

### LCD is blank

* Check VCC and GND connections.
* Check SDA → A4.
* Check SCL → A5.
* Check LCD contrast.
* Check the I2C address. `0x27` is common and `0x3F` is another common address.

### Temperature value is incorrect

* Check the LM35 orientation.
* Make sure LM35 OUT is connected to A0.
* Verify the sensor pin arrangement.

### Serial Monitor is empty

* Check the selected COM port.
* Make sure the baud rate is **9600**.

## 📸 Project Evidence

Add the following to this repository:

* Circuit photograph/screenshot
* Arduino IDE code screenshot
* Serial Monitor screenshot
* 30–60 second project demonstration video

## 🎥 Video Demonstration

**Video Link:** Add your video link here.

The demonstration should show:

**Complete Circuit → Power Arduino → LCD Temperature Reading → Serial Monitor**

## ✅ Result

The temperature monitoring system successfully reads the LM35 sensor output using Arduino UNO, displays the calculated temperature on a 16×2 I2C LCD, and logs the readings through the Serial Monitor.

## 👨‍💻 Project

**Project:** Temperature Monitoring System
**Controller:** Arduino UNO
**Sensor:** LM35
**Display:** 16×2 I2C LCD
**Serial Communication:** 9600 baud
