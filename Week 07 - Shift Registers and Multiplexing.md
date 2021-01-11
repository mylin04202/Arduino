# Week 07 - Shift Registers and Multiplexing

## Research

https://learn.adafruit.com/adafruit-arduino-lesson-4-eight-leds/overview
https://en.wikipedia.org/wiki/Bitwise_operation
https://www.arduino.cc/reference/en/#structure
 https://www.arduino.cc/en/tutorial/ShiftOut 
 www.cs.uregina.ca/Links/class-info/207/Lab8/

![image](https://www.cs.uregina.ca/Links/class-info/207/Lab8/Pictures/shift_reg_schem2_schem.png)
![image](https://www.cs.uregina.ca/Links/class-info/207/Lab8/Pictures/shift_reg_curves_bb.png)
![image](https://www.cs.uregina.ca/Links/class-info/207/Lab8/Pictures/shiftRegPlain.png)

## Tutorial

![image](https://cdn-learn.adafruit.com/assets/assets/000/002/106/large1024/learn_arduino_fritzing1.jpg?1396779311)

the chip is of a type called a shift register.

![image](https://learn.adafruit.com/assets/2109)
![image](https://cdn-learn.adafruit.com/assets/assets/000/002/109/large1024/learn_arduino_shift_register.png?1396779445)

#### note:

The shift register holds what can be thought of as eight memory locations, each of which can be a 1 or a 0.

To set each of these values on or off, we feed in the data using the 'Data' and 'Clock' pins of the chip.

The clock pin needs to receive eight pulses. At the time of each pulse, if the data pin is high, then a 1 gets pushed into the shift register. Otherwise, it is a 0. When all eight pulses have been received, then enabling the 'Latch' pin copies those eight values to the latch register. This is necessary, otherwise the wrong LEDs would flicker as the data was being loaded into the shift register.

The chip also has an OE (output enable) pin, this is used to enable or disable the outputs all at once. You could attach this to a PWM capable Arduino pin and use 'analogWrite' to control the brightness of the LEDs. This pin is active low, so we tie it to GND···

#### Arduino Code Example:

```
/*
Adafruit Arduino - Lesson 4. 8 LEDs and a Shift Register
*/
 
int latchPin = 5;
int clockPin = 6;
int dataPin = 4;
 
byte leds = 0;
 
void setup() 
{
  pinMode(latchPin, OUTPUT);
  pinMode(dataPin, OUTPUT);  
  pinMode(clockPin, OUTPUT);
}
 
void loop() 
{
  leds = 0;
  updateShiftRegister();
  delay(500);
  for (int i = 0; i < 8; i++)
  {
    bitSet(leds, i);
    updateShiftRegister();
    delay(500);
  }
}
 
void updateShiftRegister()
{
   digitalWrite(latchPin, LOW);
   shiftOut(dataPin, clockPin, LSBFIRST, leds);
   digitalWrite(latchPin, HIGH);
}

```

##### Brightness Control Eample

One pin of the 74HC595 that I have not mentioned is a pin called 'Output Enable'. This is pin 13 and on the breadboard, it is permanently connected to Ground. This pin acts as a switch, that can enable or disable the outputs - the only thing to watch for is it is 'active low' (connect to ground to enable). So, if it is connected to 5V, all the outputs go off. Whereas if it is connected to Ground, those outputs that are supposed to be on are on and those that should be off are off.

We can use this pin along with the 'analogWrite' function, that we used back in Lesson 3, to control the brightness of the LEDs using PWM (also see Lesson 3).

To do this, all you need to do, is to change the connection to pin 13 of the 74HC595 so that instead of connecting it to Ground, you connect it to pin 3 of the Arduino.

The sketch below, will once all the LEDs have been lit gradually fade them back to off.

```

int latchPin = 5;
int clockPin = 6;
int dataPin = 4;
int outputEnablePin = 3;
 
byte leds = 0;
 
void setup() 
{
  pinMode(latchPin, OUTPUT);
  pinMode(dataPin, OUTPUT);  
  pinMode(clockPin, OUTPUT);
  pinMode(outputEnablePin, OUTPUT); 
}
 
void loop() 
{
  setBrightness(255);
  leds = 0;
  updateShiftRegister();
  delay(500);
  for (int i = 0; i < 8; i++)
  {
    bitSet(leds, i);
    updateShiftRegister();
    delay(500);
  }
  for (byte b = 255; b > 0; b--)
  {
    setBrightness(b);
    delay(50);
  }
}
 
void updateShiftRegister()
{
   digitalWrite(latchPin, LOW);
   shiftOut(dataPin, clockPin, LSBFIRST, leds);
   digitalWrite(latchPin, HIGH);
}
 
void setBrightness(byte brightness) // 0 to 255
{
  analogWrite(outputEnablePin, 255-brightness);
}
```

#### Lab01

Homework Link： https://youtu.be/VsfLNeirFtc

#### Lab02

Homework Link： https://youtu.be/Q8jcBY_OGSs
