Bluetooth Controlled LED with Arduino
Overview
This project demonstrates how to control an LED using an Arduino Uno and a Bluetooth module. The Bluetooth module allows you to send commands wirelessly from a smartphone or computer to the Arduino, enabling you to control the LED (turn it on or off).

Components Used
Arduino Uno: A microcontroller that handles the control and logic.

HC-05 Bluetooth Module: Enables wireless communication between the Arduino and a smartphone or other Bluetooth device.

LED: A simple LED connected to the Arduino, used as the output device.

Resistor: A 220Ω resistor to limit current to the LED.

Circuit Diagram
Below is the basic wiring for the project:

LED:

Anode (long leg) connected to Digital Pin 13.

Cathode (short leg) connected to GND via a 220Ω resistor.

Bluetooth Module (HC-05):

TX (Transmitter) connected to RX (pin 10) on Arduino.

RX (Receiver) connected to TX (pin 11) on Arduino.

VCC and GND connected to the Arduino's 5V and GND respectively.

Arduino Code
Here’s the code you need to upload to the Arduino board to control the LED via Bluetooth:

cpp
Copy
Edit
// Define the pin for the LED
const int ledPin = 13; // Pin connected to the LED

// Include the SoftwareSerial library to communicate with the Bluetooth module
#include <SoftwareSerial.h>

// Initialize Bluetooth serial communication on pins 10 (RX) and 11 (TX)
SoftwareSerial BTSerial(10, 11); // RX, TX pins for Bluetooth module

void setup() {
  // Start serial communication for debugging and Bluetooth communication
  Serial.begin(9600);
  BTSerial.begin(9600);
  
  // Set the LED pin as an output
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // Check if there is any data coming from the Bluetooth module
  if (BTSerial.available()) {
    char command = BTSerial.read(); // Read the incoming data
    
    // If the command is '1', turn the LED on
    if (command == '1') {
      digitalWrite(ledPin, HIGH);  // LED ON
      Serial.println("LED ON");
    }
    
    // If the command is '0', turn the LED off
    if (command == '0') {
      digitalWrite(ledPin, LOW);   // LED OFF
      Serial.println("LED OFF");
    }
  }
}
Code Explanation:
Pin Definitions: The LED is connected to Digital Pin 13.

Bluetooth Communication Setup:

The SoftwareSerial library is used to create serial communication between the Arduino and the Bluetooth module. We set the Bluetooth TX pin to Arduino's RX pin (pin 10), and Bluetooth RX pin to Arduino's TX pin (pin 11).

Setup Function:

Initializes serial communication with the Bluetooth module and the Arduino serial monitor.

Sets the LED pin as an output.

Loop Function:

Continuously checks if there is data from the Bluetooth module.

If the command '1' is received, the LED turns on. If the command '0' is received, the LED turns off.

How to Use
Upload the Code: Upload the above code to your Arduino Uno using the Arduino IDE.

Connect to Bluetooth: Pair your smartphone with the Bluetooth module (HC-05).

Control the LED:

Use a Bluetooth terminal app on your smartphone to send commands:

Send 1 to turn the LED on.

Send 0 to turn the LED off.
