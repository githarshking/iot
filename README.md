# IoT Communication Protocols Lab Experiments

> **Reference:** The following experiments are extracted from the file `BCO701_LAB-MANUAL.docx`.

## General Steps to Execute Arduino Programs
Follow these steps to run any of the experiments below using the Arduino IDE:

1. **Install Arduino IDE:** Download and install the Arduino IDE from the official Arduino website if you haven't already.
2. **Connect the Board:** Use a USB cable to connect your Arduino board (e.g., Arduino UNO, NodeMCU) to your computer.
3. **Open the IDE:** Launch the Arduino IDE on your computer.
4. **Select the Board:** Go to **Tools > Board** and select your specific board model (e.g., "Arduino Uno" or "NodeMCU 1.0 (ESP-12E Module)").
5. **Select the Port:** Go to **Tools > Port** and select the COM port your board is connected to.
6. **Paste the Code:** Copy the source code provided in the experiment and paste it into the IDE editor, replacing any existing code.
7. **Verify/Compile:** Click the **Verify** button (checkmark icon in the top left) to check the code for syntax errors. 
8. **Upload:** Click the **Upload** button (right-arrow icon next to Verify) to compile and send the code to your Arduino board.
9. **View Output:** If the experiment requires it, open the **Serial Monitor** (magnifying glass icon in the top right) and ensure the baud rate matches the one in the code (e.g., `9600`).

---

## Experiment 2: Controlling the Light Emitting Diode (LED) with a Push Button

**Aim:**

To control an LED using a push button with Arduino UNO.

### Components Required

* Arduino UNO

* Push Button

* LED

* Resistor (10kΩ)

* Breadboard

* USB Cable

* Jumper Wires

### Circuit Diagram Connection

* Push button connected to digital pin 4 with a 10kΩ pull-down resistor.

* LED connected to digital pin 13.

### Source Code (Embedded C)

```cpp
const int buttonPin = 4;     // Push button connected to digital pin 4
const int ledPin = 13;       // LED connected to digital pin 13
int buttonState = 0;

void setup() {
  pinMode(ledPin, OUTPUT);
  pinMode(buttonPin, INPUT);
}

void loop() {
  buttonState = digitalRead(buttonPin);
  
  if (buttonState == HIGH) {
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }
}
```

**Result:**

Controlling LED by pressing the push button using Arduino UNO has been successfully executed.

## Experiment 3: Detection of Light Using Photoresistor (LDR)

**Aim:**

To detect the intensity of light using a photoresistor (LDR) and display the result using an Arduino.

**Objective:**

* To interface an LDR (photoresistor) with Arduino.

* To measure light levels and indicate brightness or darkness.

* To understand analog input from sensors.

### Components Required

| Component | Quantity | 
| ----- | ----- | 
| Arduino UNO | 1 | 
| LDR (Photoresistor) | 1 | 
| 10kΩ Resistor | 1 | 
| Breadboard | 1 | 
| Jumper Wires | As required | 
| USB Cable | 1 | 
| PC with Arduino IDE | 1 | 

### Circuit Diagram Connection

* One end of the LDR to 5V.

* The other end of the LDR to A0 (Analog pin) and also connected to GND via a 10kΩ resistor.

### Procedure

1. Connect the LDR and 10kΩ resistor in a voltage divider circuit as shown.

2. Connect the junction of LDR and resistor to analog pin A0 of Arduino.

3. Upload the program to Arduino using Arduino IDE.

4. Open the Serial Monitor to observe the light intensity values.

5. Observe change in values when light is varied (e.g., cover LDR with hand).

### Source Code (Arduino)

```cpp
// LDR Light Detection Program
int ldrPin = A0;      // LDR connected to analog pin A0
int ldrValue = 0;     // Variable to store LDR value

void setup() {
  Serial.begin(9600); // Start serial communication
  pinMode(ldrPin, INPUT);
}

void loop() {
  ldrValue = analogRead(ldrPin); // Read LDR value
  
  Serial.print("Light Intensity: ");
  Serial.println(ldrValue); // Display the LDR value
  
  delay(1000); // Wait for 1 second
}
```

### Input/Output Observations

| Light Condition | LDR Value Range (Approx.) | 
| ----- | ----- | 
| Bright Light | 800 - 1023 | 
| Normal Light | 400 - 800 | 
| Darkness/Shadow | 0 - 400 | 

**Result:**

The LDR successfully detected varying light levels and printed corresponding analog values to the Serial Monitor.

**Viva Questions:**

1. What is the working principle of an LDR?

2. What is the range of analog values returned by `analogRead()` in Arduino?

3. What kind of sensor is an LDR – digital or analog?

4. What is the role of the 10kΩ resistor in this circuit?

5. How can LDR be used in a real-time IoT application?

## Experiment 4: Interfacing of Temperature Sensor LM35 with Arduino

**Aim:**

To interface LM35 temperature sensor with Arduino and display the temperature reading on the Serial Monitor.

**Objective:**

* To interface the LM35 analog temperature sensor with Arduino UNO.

* To measure room temperature.

* To understand analog sensor data acquisition using Arduino.

### Components Required

| Component | Quantity | 
| ----- | ----- | 
| Arduino UNO | 1 | 
| LM35 Temperature Sensor | 1 | 
| Breadboard | 1 | 
| Jumper Wires | As required | 
| USB Cable | 1 | 
| PC with Arduino IDE | 1 | 

### Circuit Diagram Connection

* **VCC (Pin 1)** → Connect to 5V on Arduino

* **Output (Pin 2)** → Connect to A0 (Analog pin on Arduino)

* **GND (Pin 3)** → Connect to GND on Arduino

### Procedure

1. Place the LM35 sensor on the breadboard.

2. Connect VCC pin of LM35 to 5V on Arduino.

3. Connect GND pin of LM35 to GND on Arduino.

4. Connect output pin of LM35 to analog input pin A0 of Arduino.

5. Upload the Arduino code.

6. Open Serial Monitor to read temperature values.

### Source Code (Arduino)

```cpp
// LM35 Temperature Sensor Interfacing
const int lm35Pin = A0; // LM35 output connected to analog pin A0
float tempC;

void setup() {
  Serial.begin(9600); // Start serial communication
}

void loop() {
  int analogValue = analogRead(lm35Pin); // Read the analog value
  tempC = (analogValue * 5.0 * 100.0) / 1024.0; // Convert to temperature in °C
  
  Serial.print("Temperature: ");
  Serial.print(tempC);
  Serial.println(" °C");
  
  delay(1000); // Wait for 1 second
}
```

### Calculation Logic

* LM35 provides 10mV per °C.

* Arduino ADC gives a value between 0–1023 for 0–5V.

* **Formula:** Temperature (°C) = `(analogRead × 5.0 × 100) / 1024`

### Input/Output Observations

| Analog Reading | Temperature (°C) | 
| ----- | ----- | 
| 102 | \~50 | 
| 205 | \~100 | 
| 307 | \~150 | 
| 410 | \~200 | 

**Result:**

The LM35 temperature sensor was successfully interfaced with Arduino, and real-time temperature data was displayed on the Serial Monitor.

**Viva Questions:**

1. What is the sensitivity of the LM35 sensor?

2. How is temperature calculated from the analog value in LM35?

3. What is the resolution of the Arduino ADC?

4. Can LM35 measure negative temperatures?

5. Why do we multiply by 100 in the conversion formula?

## Experiment 5: Interfacing Motor Using Relay with Arduino

**Aim:**

Write a program to turn ON motor when push button is pressed using relay with Arduino UNO.

### Components Required

* Arduino UNO

* Relay

* Resistor (10kΩ)

* Motor

* Connecting cable or USB cable

* Breadboard

* Jumper wires

### Source Code (Embedded C)

```cpp
#define RELAY_PIN 8  // Digital pin connected to the relay module 
#define BUTTON_PIN 2 // Digital pin connected to the push button 

void setup() {
  Serial.begin(9600); 
  pinMode(RELAY_PIN, OUTPUT); 
  pinMode(BUTTON_PIN, INPUT);
}

void loop() {
  int buttonState = digitalRead(BUTTON_PIN);
  
  if (buttonState == HIGH) {
    // Button is pressed, turn ON the motor via relay 
    digitalWrite(RELAY_PIN, HIGH);
    delay(1000); // Delay for motor ON time (1 second in this case)
  } else {
    // Button is not pressed, turn OFF the motor via relay 
    digitalWrite(RELAY_PIN, LOW);
  }
}
```

**Result:**

Motor turn ON/OFF operation when push button is pressed using relay with Arduino UNO has successfully executed.
