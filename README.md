# sridhar G (212223060271)
# EXP 1(A) FAN SPEED CONTROLLER SYSTEM USING TEMPERATURE SENSOR

# Aim:
To measure the Temperature using DHT11/DHT22/TMP36  sensor with Arduino UNO Board/ESP-32
using Tinker CAD.

# Hardware / Software Tools required:
- PC/ Laptop with Internet connection
- Tinker CAD tool (Online)
- Arduino UNO Board/ESP-32
- Temperature Sensor (DHT11/DHT22/TMP36)

# Schematic view:

<img width="964" height="732" alt="Screenshot 2025-09-02 134051" src="https://github.com/user-attachments/assets/518d8b87-d84e-4205-a074-97fffe28c8d5" />

# Circuit Diagram:

<img width="1164" height="726" alt="Screenshot 2025-09-02 134958" src="https://github.com/user-attachments/assets/70857cf1-e8ba-46cc-961f-c66db004be15" />

# Procedure

Step 1: Set Up the Tinkercad Environment
1.	Log in to Tinkercad: Open Tinkercad in your web browser and log in to your account.
2.	Create a New Circuit: In the Tinkercad dashboard, click on "Circuits" and then select "Create New Circuit."
Step 2: Add Components to the Circuit
1.	Arduino Uno: Drag an Arduino Uno board from the components panel onto the workspace.
2.	TMP36 Sensor: Search for the TMP36 sensor in the components panel and drag it into the workspace.
3.	Breadboard: Drag a small breadboard to the workspace to help with wiring connections.
4.	Resistor (Optional): A resistor may not be necessary for this simple setup, but you can include it for more accurate readings.
5.	Wires: Use wires to connect the components.

Step 3: Connect the TMP36 Sensor to the Arduino
1.	TMP36 Pins:
o	Vout (Middle Pin): Connect this to an analog input pin on the Arduino (e.g., A0).
o	GND (Right Pin): Connect this pin to the ground (GND) on the Arduino.
o	Vs (Left Pin): Connect this to the 5V pin on the Arduino.
2.	Breadboard Wiring:
o	TMP36 Vout (Middle Pin) to Arduino A0: Use a wire to connect the middle pin (Vout) of the TMP36 sensor to the A0 analog input pin on the Arduino.
o	TMP36 GND (Right Pin) to Breadboard GND Rail: Connect the GND pin of the TMP36 sensor to the ground rail of the breadboard.
o	TMP36 Vs (Left Pin) to Breadboard 5V Rail: Connect the Vs pin of the TMP36 sensor to the 5V rail of the breadboard.
o	Arduino GND to Breadboard GND Rail: Connect a wire from the Arduino GND pin to the ground rail on the breadboard.
o	Arduino 5V to Breadboard 5V Rail: Connect a wire from the Arduino 5V pin to the power rail on the breadboard.

Step 4: Write the Arduino Code
1.	Code Editor: Click on the "Code" button at the top of the Tinkercad workspace to open the code editor.
2.	Set the Coding Mode: Ensure the editor is in "Text" mode to write your code in C/C++.
3.	Enter the Code: Write the following code to read the temperature from the TMP36 sensor
   
Step 5: Simulate the Circuit
1.	Start Simulation: Click the "Start Simulation" button at the top of the workspace to run the circuit and code.
2.	Monitor Output: Open the serial monitor by clicking the "Serial Monitor" button to view the temperature readings in both Celsius and Fahrenheit.
   
Step 6: Troubleshoot and Refine
1.	Check Connections: Ensure that all connections are made correctly on the breadboard and the Arduino.
2.	Adjust Code: If needed, tweak the code to improve accuracy or change the format of the output.
   
Step 7: Save Your Work
1.	Stop Simulation: Click "Stop Simulation" to end the simulation.
2.	Save the Circuit: Click "Save" to keep your circuit design and code for future use.


# Program
```
#include <LiquidCrystal.h>

// LCD pin mapping: (RS, E, D4, D5, D6, D7)
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

const int tempPin = A0;      // TMP36 output pin
const int motorPin = 9;      // Motor PWM pin
const int ledPin = 7;        // LED pin

void setup() {
  pinMode(motorPin, OUTPUT);
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);

  // Initialize LCD
  lcd.begin(16, 2);
  lcd.print("Temp & Motor");
  delay(2000);
  lcd.clear();
}

void loop() {
  int sensorValue = analogRead(tempPin);
  
  // Convert TMP36 reading to temperature in Celsius
  float voltage = sensorValue * (5.0 / 1023.0);
  float temperatureC = (voltage - 0.5) * 100.0;

  // Map temperature to PWM speed (20°C = stop, 40°C = full speed)
  int motorSpeed = map(temperatureC, 20, 40, 0, 255);
  motorSpeed = constrain(motorSpeed, 0, 255);

  analogWrite(motorPin, motorSpeed);

  // LED indicator ON if motor running
  if (motorSpeed > 0) {
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }

  // Display on Serial Monitor
  Serial.print("Temperature: ");
  Serial.print(temperatureC);
  Serial.print(" C, Motor Speed: ");
  Serial.println(motorSpeed);

  // Display on LCD
  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(temperatureC);
  lcd.print("C   ");

  lcd.setCursor(0, 1);
  lcd.print("Speed: ");
  lcd.print(motorSpeed);
  lcd.print("   ");

  delay(500);
}

```
# OUTPUT
https://github.com/user-attachments/assets/84b814c4-a8c2-4df0-b5f0-cf488af372e0

# RESULT
FAN SPEED CONTROLLER SYSTEM USING TEMPERATURE SENSOR USING TINKERCAD EXECUTED SUCCESSfully.
