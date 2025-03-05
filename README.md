# BAE305-SP25-Lab5
# Laboratory Report for Lab 5 of BAE305 Spring 2025
# Lab 5 - The Brain: Microcontrollers 
* By: Abby Phillips and Audrey Suit
* Submitted: March 5, 2025


# Summary  

# Materials
•	Computer running Arduino IDE
•	SparkFun Inventor’s kit: RedBoard, Photoresistor, an LED, 10 kΩ potentiometer, 10 kΩ and 330Ω resistors

# Assembly Procedures  

Using the Fluke digital multimeter, we measured the actual resistance of the 10 kΩ and 330Ω resistors by attaching the multimeter probes to their terminals with alligator clips. The labeled resistance was verified using the resistor color code.

### Part 1 - Blinking an LED

To assemble the Arduino system, we peeled and stuck the breadboard to the devoted section of the Sparkfun base and screwed the Redboard to the other section of the Sparkfun base.
After starting Arduino IDE on the computer, we selected our Arduino Uno following the menu (Tools>Board>Arduino Uno) and connected the corresponding COM port through (Tools>Port>COM1).
Next we downloaded the blink program following the menus (File>Examples>Basics>Blink) and downloaded it to the Arduino.
We assembled the circuit on our breadboard, consisting of a 330Ω resistor and an LED in series to pin 13 in our RedBoard. This is shown in the Figures 1.1 and 1.2 below.

insert schematic 

insert circuit photo

The blink program is used to test part 1, as detailed below in the Test Procedures section of this lab report. 

### Part 2 - Controlling an LED with a Potentiometer

For this portion of the lab, we kept the circuit built in Part 1. We connected our potentiometer to 5V and Ground, as well as connecting the variable resistance pin to A0. This setup can be viewed in Figures 2.1 and 2.2 below.

insert schematic

insert circuit photo


# Test Equipment
•	Oscilloscope
•	Fluke Digital Multimeter

# Test Procedures
## Part 1: Blinking an LED
1. Assemble the Circuit by attaching the RedBoard and breadboard to the SparkFun base. Connect the RedBoard to the computer using a USB cable.
2. Setup Arduino IDE
  - Select Tools > Board > Arduino Uno.
  - Select the correct COM port (Tools > Port > COM?).
3. Upload and Run the Blink Program
  - Open the Blink program (File > Examples > Basics > Blink).
  - Click Upload to transfer the program to the Arduino.
  - Observe the LED blinking.
4. Modify the Delay
  - Reduce the delay time until the LED appears to stay constantly illuminated.
  - Record the minimum delay at which the LED appears constant (12ms).
5. Consider: How does persistence of vision apply to this observation? Where is this phenomenon used in real-world applications (e.g., electronics, computer screens)?

## Part 2: Controlling an LED with a Potentiometer
1. Load the Analog Read Serial Program
  - Open File > Examples > Basics > AnalogReadSerial.
  - Upload the program to the Arduino.
2. Modify the Circuit
  - Connect the potentiometer: 5V to one end, Ground (GND) to the other end, Middle (variable resistance) pin to A0.
  - Verify operation using Tools > Serial Monitor (9600 bps).
3. Modify the Code
  - Include LED control based on potentiometer input.
  - Set blinking delay to match potentiometer readings.
4. Consider: Difference between analog and digital signals, Examples of real-world analog signals
5. Observe serial monitor refresh rates as the potentiometer is adjusted.

## Part 3: Controlling an LED with a Photoresistor
1. Modify the Circuit
  - Replace potentiometer with a photoresistor.
  - Connect photoresistor in series with a 10 kΩ resistor.
  - 5V to photoresistor, Ground to resistor.
  - A0 to the node between them.
2. Test Light Sensitivity
  - Observe minimum and maximum analog values:
3. Modify Code for Light-Based LED Control
  - Implement if-else statement to turn LED on when brightness is low:
4. Observe: How does the LED respond when light is blocked and unblocked?
5. Consider: Why does the LED turn on/off immediately?

## Part 4: LED Dimmer Using PWM
1. Modify the Circuit
  - Use the potentiometer circuit from Part 2.
  - Connect LED to a PWM-capable pin (e.g., Pin 6).
2. Modify the Code
  - Map potentiometer voltage (0-1023) to PWM values (0-255):
3. Oscilloscope Analysis
  - Connect an oscilloscope to the LED pin.
  - Observe changes in duty cycle and LED brightness as the potentiometer is adjusted.
4. Consider: Relationship between duty cycle and LED brightness. Explanation of PWM mapping and its effect on mean voltage.

# Test Results
## Part 1: Blinking an LED
```ruby
// the setup function sets up the arduino code after resetting
void setup() {
  pinMode(LED_BUILTIN, OUTPUT); // initialize digital pin LED_BUILTIN as an output.
}

// the loop function runs over and over again forever and performs function
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  // turn the LED on (HIGH is the voltage level)
  delay(1000);                      // wait for a second
  digitalWrite(LED_BUILTIN, LOW);   // turn the LED off by making the voltage LOW
  delay(1000);                      // wait for a second
}
```

## Part 2: Controlling an LED with a Potentiometer
```ruby
void setup() {
  Serial.begin(9600); // initialize serial communication at 9600 bits per second
}

void loop() {
  int sensorValue = analogRead(A0);   // read the input on analog pin 0
  Serial.println(sensorValue);        // read the input on analog pin 0
  delay(1);                           // delay in between reads for stability
}
```

```ruby
void setup() {
  Serial.begin(9600);     // initialize serial communication at 9600 bits per second
  pinMode(LED_BUILTIN, OUTPUT);    // initialize digital pin LED_BUILTIN as an output.
}

void loop() {
  int sensorValue = analogRead(A0);   // read the input on analog pin 0:
  Serial.println(sensorValue);        // print out the value you read:
  delay(1);  // delay in between reads for stability

  digitalWrite(LED_BUILTIN, HIGH);  // turn the LED on (HIGH is the voltage level)
  delay(sensorValue);               // wait for a second
  digitalWrite(LED_BUILTIN, LOW);   // turn the LED off by making the voltage LOW
  delay(sensorValue);    
}
```

## Part 3: Controlling an LED with a Photoresistor
```ruby
if(sensorValue<700){
digitalWrite(LED_BUILTIN, HIGH); //turns on LED if the photoresistor value <700
}
else{
   digitalWrite(LED_BUILTIN, LOW); //turns off LED if the photoresistor value is not <700
}
```

## Part 4: LED Dimmer Using PWM
```ruby
const int ledPin=6;     //communicates to the arduino that the LED is in pin 6 on the arduino

// the setup routine runs once when you press reset:
void setup() {
 
  Serial.begin(9600);        // initialize serial communication at 9600 bits per second:
  pinMode(ledPin, OUTPUT);   // initialize digital pin LED_BUILTIN as an output.
}

// the loop routine runs over and over again forever:
void loop() {
  int sensorValue = analogRead(A0);  // read the input on analog pin 0
  Serial.println(sensorValue);       //prints out the value read by the analog signal
  delay(1);                          // delay in between reads for stability

int mappedValue = map(sensorValue, 0, 1023, 0, 255);  // maps the voltage value from 0 to 1023 to a value from 0 to 255
analogWrite(ledPin, mappedValue);  //writes the mapped value to the LED pin
}
```

# Discussion


# Conclusion

