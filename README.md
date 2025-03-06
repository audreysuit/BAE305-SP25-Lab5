# BAE305-SP25-Lab5
# Laboratory Report for Lab 5 of BAE305 Spring 2025
# Lab 5 - The Brain: Microcontrollers 
* By: Abby Phillips and Audrey Suit
* Submitted: March 5, 2025


# Summary  

In this lab, we explored the fundamentals of microcontrollers by working with the Arduino platform and the RedBoard (Arduino UNO) to control various circuit components. Our primary objective was to familiarize ourselves with the Arduino IDE and the process of programming microcontrollers. We began by uploading a simple “Blink” program to turn an LED on and off, which confirmed that our hardware and code were working properly. Next, we advanced to reading analog inputs by connecting a potentiometer and using the Arduino’s analog-to-digital converter, allowing us to adjust the LED’s blinking rate. We then replaced the potentiometer with a photoresistor in combination with a fixed resistor to monitor light levels, using an if-else structure in our code to operate the LED as a night light. Finally, we implemented pulse width modulation (PWM) to control LED brightness by mapping analog sensor values to a 0–255 PWM range. Through these exercises, we reinforced our understanding of digital versus analog signals, the structure of Arduino programs (declarations, setup, and loop), and how PWM can simulate varying analog outputs. This lab provided a solid foundation in microcontroller programming and sensor interfacing, preparing us for more complex projects in the future.

# Materials
- Computer running Arduino IDE
- SparkFun Inventor’s kit: RedBoard, Photoresistor, an LED, 10 kΩ potentiometer, 10 kΩ and 330Ω resistors

# Assembly Procedures  

Using the Fluke digital multimeter, we measured the actual resistance of the 10 kΩ and 330Ω resistors by attaching the multimeter probes to their terminals with alligator clips. The labeled resistance was verified using the resistor color code.

### Part 1 - Blinking an LED

To assemble the Arduino system, we peeled and stuck the breadboard to the devoted section of the Sparkfun base and screwed the Redboard to the other section of the Sparkfun base.
After starting Arduino IDE on the computer, we selected our Arduino Uno following the menu (Tools>Board>Arduino Uno) and connected the corresponding COM port through (Tools>Port>COM1).
Next we downloaded the blink program following the menus (File>Examples>Basics>Blink) and downloaded it to the Arduino.
We assembled the circuit on our breadboard, consisting of a 330Ω resistor and an LED in series to pin 13 in our RedBoard. This is shown in the Figures 1.1 and 1.2 below.

insert schematic 

![image](https://github.com/user-attachments/assets/d383f177-02c1-4c2d-84b9-7377477f4d0f)


The blink program is used to test part 1, as detailed below in the Test Procedures section of this lab report. 

### Part 2 - Controlling an LED with a Potentiometer

For this portion of the lab, we kept the circuit built in Part 1. We connected our potentiometer to 5V and Ground, as well as connecting the variable resistance pin to A0. This setup can be viewed in Figures 2.1 and 2.2 below.

insert schematic

![image](https://github.com/user-attachments/assets/fe79602c-a8e2-4798-8853-eb123834f1e3)

To ensure this system was working properly, we used the Serial Monitor tool to verify that the Baud rate was set at 9600 bps. This set us up to run tests described below in the Test Procedures.

### Part 3 - Controlling an LED with a Photoresistor

In this section of the lab, we kept the circuit from previous parts but replaced the potentiometer with a photoresistor in series with a 10 kΩ resistor. We connected the photoresistor to 5V, the resistor to ground, and ran a wire from A0 to the node between the photoresistor and 10 kΩ resistor. See Figures 3.1 and 3.2 below for the schematic and image of this circuit setup.

insert schematic

![image](https://github.com/user-attachments/assets/72ced225-27d5-48db-a8b8-7125b6285aa4)


### Part 4 - LED Dimmer using PWM

For this part, we used the circuit from part 2 (reference Figures 2.1 and 2.2) changing the LED to one that is PWM capable. After configuring this setup, we connected the oscilloscope to the LED pin by connected the probe leads to the LED and the wire on the other side of the LED. This is shown in Figure 4.1 below.

insert circuit photo

# Test Equipment
- Oscilloscope
- Fluke Digital Multimeter

# Test Procedures
## Part 1: Blinking an LED
1. Assemble the Circuit by attaching the RedBoard and breadboard to the SparkFun base. Connect the RedBoard to the computer using a USB cable.
2. Setup Arduino IDE
    - Select Tools > Board > Arduino Uno.
    - Select the correct COM port (Tools > Port > COM?). In our case, we connected to COM3. 
3. Upload and Run the Blink Program
    - Open the Blink program (File > Examples > Basics > Blink).
    - Click Upload to transfer the program to the Arduino. The code will automatically verify when uploaded so no need to do it separately.
    - Create Circuit 1 on the RedBoard and connect power via your computer. The LED should flash.
4. Modify the Delay
    - Reduce the delay time by decreasing the value in delay() function until the LED appears to stay constantly illuminated.
    - Record the minimum delay at which the LED appears constant.
5. Consider: How does persistence of vision apply to this observation? Where is this phenomenon used in real-world applications (e.g., electronics, computer screens)?

## Part 2: Controlling an LED with a Potentiometer
1. Load the Analog Read Serial Program
    - Open File > Examples > Basics > AnalogReadSerial.
    - Upload the program to the Arduino.
2. Modify the Circuit
    - Connect the potentiometer: 5V to one end, Ground (GND) to the other end, Middle (variable resistance) pin to A0, leaving the rest of Circuit 1 intact. This is shown in Circuit 2 in the Assembly procedures
    - Verify operation using Tools > Serial Monitor (9600 bps) and make sure the Baud Rate is 9600 bps
3. Modify the Code
    - Include LED control based on potentiometer input.
    - Set blinking delay to match potentiometer readings.
    - Confirm code is working by adjusting the potentiometer
4. Consider: Difference between analog and digital signals, Examples of real-world analog signals
5. Observe serial monitor refresh rates as the potentiometer is adjusted.

## Part 3: Controlling an LED with a Photoresistor
1. Modify the Circuit
    - Replace potentiometer with a photoresistor.
    - Connect photoresistor in series with a 10 kΩ resistor.
    - 5V to photoresistor, Ground to resistor.
    - A0 to the node between them.
    - NOTE: Analog input should be connected to the node between the photodetector and resistor.
2. Test Light Sensitivity
    - Observe minimum and maximum analog values
3. Modify Code for Light-Based LED Control
    - Implement if-else statement to turn LED on when brightness is low as shown in Program 3.
4. Observe: How does the LED respond when light is blocked and unblocked?
5. Consider: Why does the LED turn on/off immediately?

## Part 4: LED Dimmer Using PWM
1. Modify the Circuit
    - Use the potentiometer circuit from Part 2.
    - Change LED pin to a PWM-capable pin (e.g., Pin 6).
2. Modify the Code
    - Map potentiometer voltage (0-1023) to PWM values (0-255) as shown in Program 4.
3. Oscilloscope Analysis
    - Connect an oscilloscope to the LED pin.
    - Observe changes in duty cycle and LED brightness as the potentiometer is adjusted.
    - We used the SEC/DIV and and channel adjustment knobs to make a clear image on the oscilloscope.
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
<p align="left"><em> Program 1: The above program turns the LED on and off in the loop function by making the voltage level high and low, respectively. This runs over and over again until the board is turned off or a new code is uploaded. It does this after initializing the digital pin LED_BUILTIN as an output in the setup function after resetting or powering the board. </em></p>

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
<p align="left"><em> Program 2.1: The above program starts serial communication at a rate of 9600 bits per second, allowing the Arduino to send data to the computer. The loop function then reads a voltage level from pin A0, the potentiometer, and then prints the value to the serial monitor.  </em></p>

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
<p align="left"><em> Program 2.2: The above program displays the voltage levels as shown in Program 2.1, and then turns an LED on and off for a duration equal to the sensorValue read from pin A0 (the potentiometer). The cylce then repeats in a loop until a new code is uploaded or power is turned off. </em></p>

## Part 3: Controlling an LED with a Photoresistor
```ruby
if(sensorValue<700){
digitalWrite(LED_BUILTIN, HIGH); //turns on LED if the photoresistor value <700
}
else{
   digitalWrite(LED_BUILTIN, LOW); //turns off LED if the photoresistor value is not <700
}
```
<p align="left"><em> Program 3: The above program is a conditional statement that controls an LED based on the value of a photoresistor. Functioning like a night light, this program turns on an LED only when the brightness sensed by the photoresistor is low (<700). We determined this value by analyzing the darkest (500) and brightest (1015) readings of the photoresistor using the serial monitor. </em></p>

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
<p align="left"><em> Program 4: The above program reads an analog input from pin A0 (the potentiometer) as demonstrated by program 2.1 and 2.2, and then maps the value to a PWM signal to control the brightness of the LED. The map function scales the sensor reading from 0-1023 (analog) to 0-255 (PWM).  </em></p>

**Oscilloscope Images for Varying Potentiometer Values**
| Decreased Value  | Increased Value|
|--------------------|--------------------|
|![image](https://github.com/user-attachments/assets/7f8d18f4-9c21-4adc-abc5-15c6a6e0c120) |![image](https://github.com/user-attachments/assets/fd4a78e3-c9e6-4da1-b699-292fe43f1235) |

<p align="left"><em> Table 1: Oscilloscope images for low and high potentiometer sensor values are shown above. As demonstrated, when potentiometer value is increased, the duty cycle (shown by width of peaks) increases. When the potentiometer value decreases, the duty cycle decreases.  </em></p>

# Discussion

Discussion Question 1: Your LED flashes with a delay from the uploaded code. Decrease this delay (after both write instructions) until the LED just stops blinking--that is the light is still blinking but appears to stay constantly illuminated. What is the value of your delay? What field may this "persistance of vision" play a greater role in?

The value of the delay to cause the LED to appear constantly illuminated whilst blinking was 12 ms. This plays a greater role in electronics and screens used for computers, televisions and smartphones. The persistence of vision phenomenon, where rapid blinking or changing images appear as continuous to the human eye, is crucial in electronics and display technology. These screens refresh images that we perceive as smooth and continuous rather than flashing individual images.

Discussion Question 2a: What is the difference between an analog and a digital signal?

An analog signal is produced continuously while digital produces a blinking signal that typically reads either 0 or 1.

Discussion Question 2b: List a few examples of real-world examples that can be described by an analog signal. Likewise, what are the two states which can be conveyed by a digital signal?

An example of a real world analog signal may be a light sensor. As we've seen, a device like a photoresistor or photodiode produces an analog signal that varies with changes in light intensity. Other examples are found in the medical field, like electrocardiograms (ECGs) and respiratory signals. ECGs record continuous electrical signals in the heart and brain. Respiratory signals record from airflow sensors to capture breathing patterns and volumes.

Discussion Question 2c: What happens to the Serial Monitor Refresh rate as you move the potentiometer to control the LED blinking time? 

The refresh rate decreases as you increase the potentiometer value, because it communicates a higher signal directly to the delay function. This lows down the blinking of the LED since it increases the values of the serial monitor. This is because the delay is directly tied to the sensor value. When we decrease the sensor value, it decreases the delay, and increases refresh rate.

Discussion Question 3: Does the LED turn on immediately after blocking the light? What about when you remove the object blocking the light, does the LED turn off immediately? Why? 

Yes, the light turns on and off immediately. The code is constantly running the if-else statement to read the input value, so when the input value is below/above the threshold (700), the LED quickly turns on and off. There would be a slight delay if we decreased the rate of the serial monitor or delay on the readings, but since it is monitoring at 9600 bps, the delay is not visible.

Discussion Question 4: Connect the oscilloscope to the LED pin and observe and record what happens to the signal and the LED brightness when you turn the knob of the potentiometer.

As we increase the potentiometer, and therefore the sensor value, the LED appears brighter, and the PWM duty cycle increases since the LED stays on for a longer portion of each cycle. This is shown by an increase in width of the pulses on the oscilloscope since the duty cycle has increased. The mean voltage rises because the LED is on more frequently, hence, the increased brightness. The opposite is true when we decrease the potentiometer value, decreasing the brightness and duty cycle. This means the LED is on for a shorter period of time demonstrating a narrow pulse on the oscilloscope, decreasing the mean voltage since the LED is on for less time. PWM controls the average voltage supplied to an LED.


# Conclusion

