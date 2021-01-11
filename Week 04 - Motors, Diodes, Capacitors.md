# Week 04 - Motors, Diodes, Capacitors



## **Lab : Hook up a servo.**

### Requirement:

Hook up a servo and make it move using pwm.[Do this tutorial](https://www.instructables.com/id/Arduino-Servo-Motors/)

#### Tutorial：

We will need the following things:

1. An Arduino board connected to a computer via USB
2. A servo motor
3. Jumper wires

##### Step 1: How to Connect Them

![image](https://content.instructables.com/ORIG/FYG/SWN3/IBXMMLB3/FYGSWN3IBXMMLB3.png?auto=webp&frame=1&width=1024&fit=bounds&md=82e53a3443fd67343967a3199d2aeca0)
A servo motor has everything built in: a motor, a feedback circuit, and most important, a motor driver. It just needs one power line, one ground, and one control pin.

Following are the steps to connect a servo motor to the Arduino:

The servo motor has a female connector with three pins. The darkest or even black one is usually the ground. Connect this to the Arduino GND.
Connect the power cable that in all standards should be red to 5V on the Arduino.
Connect the remaining line on the servo connector to a digital pin on the Arduino.

##### Step 2: Code

The following code will turn a servo motor to 0 degrees, wait 1 second, then turn it to 90, wait one more second, turn it to 180, and then go back.

```
// Include the Servo library 
#include <Servo.h> 
// Declare the Servo pin 
int servoPin = 3; 
// Create a servo object 
Servo Servo1; 
void setup() { 
   // We need to attach the servo to the used pin number 
   Servo1.attach(servoPin); 
}
void loop(){ 
   // Make servo go to 0 degrees 
   Servo1.write(0); 
   delay(1000); 
   // Make servo go to 90 degrees 
   Servo1.write(90); 
   delay(1000); 
   // Make servo go to 180 degrees 
   Servo1.write(180); 
   delay(1000); 
}

```
If the servo motor is connected on another digital pin, simply change the value of servoPin to the value of the digital pin that has been used.

![image](https://content.instructables.com/ORIG/F8A/CFQ0/IBXMML86/F8ACFQ0IBXMML86.png?auto=webp&frame=1&width=1024&height=1024&fit=bounds&md=8b86c54c8d87a2798cf28dabf8d400df)

Servos are clever devices. Using just one input pin, they receive the position from the Arduino and they go there. Internally, they have a motor driver and a feedback circuit that makes sure that the servo arm reaches the desired position. But what kind of signal do they receive on the input pin?

It is a square wave similar to PWM. Each cycle in the signal lasts for 20 milliseconds and for most of the time, the value is LOW. At the beginning of each cycle, the signal is HIGH for a time between 1 and 2 milliseconds. At 1 millisecond it represents 0 degrees and at 2 milliseconds it represents 180 degrees. In between, it represents the value from 0–180. This is a very good and reliable method. The graphic makes it a little easier to understand.

Remember that using the Servo library automatically disables PWM functionality on PWM pins 9 and 10 on the Arduino UNO and similar boards.

Code breakdown
The code simply declares the servo object and then initializes the servo by using the servo.attach() function. We shouldn't forget to include the servo library. In the loop(), we set the servo to 0 degrees, wait, then set it to 90, and later to 180 degrees.


https://www.instructables.com/id/Arduino-Servo-Motors/


### VedioLink：

https://www.tinkercad.com/things/58FfKepfxFJ-mighty-blorr/editel?tenant=circuits



## **Lab : Hook up a motor**

### Requirement:

Using the circuit from the Arduino project book, do project 9. Feel free to get creative with the pinwheel bit of you want.

### Homework Vedio Link：

https://www.tinkercad.com/things/cjoY511Uv4G-week04motor/editel



## **Lab  - The Capsense library**

### Requirement:

[Give a go with this tutorial](https://playground.arduino.cc/Main/CapacitiveSensor/)What are some creative ideas you could do with this? Try one out and submit it as this lab.

### Home work Vedio Link:

https://youtu.be/ar0dfOLa0-M

### Research Material

#### Example code: Threshold
Instead of using capacitors, you may use a function to count relevant values, and reset the count when encountering lower values (interferences). This is a code example for a touch lamp. It require to either touch the pin 8 wire or to get close to an antenna, and it stops the readings when the threshold is reached. You might want to adjust values A, B and C according to your particular project.
```

#include <CapacitiveSensor.h>
CapacitiveSensor cs_7_8 = CapacitiveSensor(7,8); //10M Resistor between pins 7 and 8, you may also connect an antenna on pin 8
unsigned long csSum;

void setup() {
    Serial.begin(9600);
}

void loop() {
    CSread();
}

void CSread() {
    long cs = cs_7_8.capacitiveSensor(80); //a: Sensor resolution is set to 80
	if (cs > 100) { //b: Arbitrary number
		csSum += cs;
		Serial.println(cs); 
		if (csSum >= 3800) //c: This value is the threshold, a High value means it takes longer to trigger
		{
			Serial.print("Trigger: ");
			Serial.println(csSum);
			if (csSum > 0) { csSum = 0; } //Reset
			cs_7_8.reset_CS_AutoCal(); //Stops readings
		}
	} else {
		csSum = 0; //Timeout caused by bad readings
	}
}

```

### Videos referenced


https://www.youtube.com/watch?v=BHQPqQ_5ulc
https://www.youtube.com/watch?v=jco-uU5ZgEU
https://www.youtube.com/watch?v=stejKa03tdw
https://www.instructables.com/How-To-Use-Touch-Sensors-With-Arduino/

### F&Q about the Capsense library

*01:Why does the proximity of e.g. a human hand change the time taken for the receive pin to change state?*

   Because the proximity of the item (finger) has a charge, and affects the timing of the charge to change state.

*02:Why is a resistor needed? I can understand a small resistor, but the example seems to recommend a very large (10 Mohm or greater) resistor for better sensitivity.*

   A resistor is needed or the charge and sense pins will be shorted out i.e R=0 and thus charge time will be 0 and c = 0 Because of the formula T = R x C

   The site recommends capacitors for better performance. How do these enhance performance? Small value C will decrease noise and thus increase stability and accuracy.

*03:Does the frequency with which the send pin toggles play into the detectors performance at all?*

   Yes if you mean the value passed in the reading function capacitiveSensor(byte samples) Taking mores samples will increase sensitivity.
