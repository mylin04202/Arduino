# Week 04 - Motors, Diodes, Capacitors



## **Lab : Hook up a servo.**

### Requirement:

Hook up a servo and make it move using pwm.[Do this tutorial](https://www.instructables.com/id/Arduino-Servo-Motors/)

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
