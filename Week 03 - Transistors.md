# Week 03 - Transistors

## Lab 01: PWM

### requirement：
Today we're going to use PWM to fade an LED.

Playing with fades

- Go here and build this circuit. Try typing the code yourself: https://www.arduino.cc/en/Tutorial/Fade

Take a short video to submit of the working circuit, or put a link to your tinkercad project you've made public on your blog.

### homework link：
https://www.tinkercad.com/things/4PQAZPA3scv-week03lab01/editel
![image](https://github.com/mylin04202/img/blob/main/W03L01.jpg)

## Lab 02 Voltage Dividers

### requirement：

Hook up the circuit in the slides with the light dependent resistor. 

Take a short video to submit of the working circuit, or put a link to your tinkercad project you've made public on your blog.

https://www.tinkercad.com/things/dvBfcmGSWFj-week03lab02/editel
![image](https://github.com/mylin04202/img/blob/main/W03L02.jpg)

## Lab 03: Dark detecting Circuit

### requirement：

Making a dark detecting LED (From Circuit diagram to breadboard) Build this project to better understand transistors https://makezine.com/projects/dark-detecting-led/ There is one change though, verses use a battery, we're just going to power our circuit with the Arduino 3V out.

[Here's the datasheet for the phototransistor] (https://www.avnet.com/shop/emea/products/everlight/pt333-3c-3074457345634369228?&r=EMEA&CMP=AVNET-EMEA-PPC-Google-All-English-AVE14-SKU-1699305114-66248026957-042019)

Take a short video to submit of the working circuit, or put a link to your tinkercad project you've made public on your blog. Note in Tinkercad the phototransistor here is called an Ambient Light Sensor [Phototransistor]


#### Tutorial

##### Schematic

![image](http://cdn.makezine.com/uploads/2014/10/wp20_schematic_w_circle-transistor.png?w=1024)

You can see the circuit contains only five components: battery, phototransistor, resistor, LED, and transistor. The parts listed for this project contain variations of all of these components. You can choose a la carte the components you want for their physical or aesthetic properties, but it really boils down to these five components.

For instance, you could choose to use a 3V coin cell battery and holder, or two AA batteries in a battery pack. You could choose a directional red LED in a clear package or a diffused one in a colored package. It all depends on where you want the project to eventually live, and how discreet or embedded you want it to be. However it should be noted that this design is only guaranteed to work with the specified components. You can’t simply replace the red LED with a blue or white one, due to the differences in forward voltage (and other specifications) required by each LED. Spend some time reading up on LEDs and Ohm’s law and you’ll be experimenting in no time!

##### The Transistor

![image](http://cdn.makezine.com/uploads/2014/09/1024px-bjt_npn_symbol_case.png?w=150)
![image](https://1abxf1rh6g01lhm2riyrt55k-wpengine.netdna-ssl.com/wp-content/uploads/2014/09/img_20140930_104431_detail_letters.jpg)

The 2N3904 is a common low-power NPN transistor used in many hobby electronics projects. Unlike most simple electronics components that have two leads (typically anode and cathode; or which operate as junctions between other components, like resistors) this transistor has three leads. 1024px-BJT_NPN_symbol_(case)The “NPN” indicates the semiconductor is P-doped between two N-doped layers; as opposed to “PNP” transistors which are doped the opposite way around. The SKU 276-2016 sold by RadioShack comes in the TO-92 package configuration; one side is curved while the other is flat and has data imprinted on it (image above). The symbol for a transistor, seen at right, looks similar to the phototransistor symbol, but with that added third ‘leg’ and circle framing the symbol proper. A mnemonic for the NPN transistor’s symbol is the arrow is Not Pointing iN; again as opposed to PNP transistors whose symbol arrow Points iN Proudly.

Here’s a picture of a 2N3904 in a breadboard, with the leads indicated:

![image](https://1abxf1rh6g01lhm2riyrt55k-wpengine.netdna-ssl.com/wp-content/uploads/2014/09/img_20140930_102920_detail_letters.jpg)

When prototyping on a breadboard, a trick I use to orient the transistor properly is to imagine the symbol overlayed over the component like so:

![image](https://1abxf1rh6g01lhm2riyrt55k-wpengine.netdna-ssl.com/wp-content/uploads/2014/10/img_20140930_102920_detail_overlay2.jpg)

quickly place the leads or indicate their function. I doubt the component and symbol were designed with this in mind, but it’s a rather serendipitous visual aid nonetheless.

As shown in the schematic above, when photons (particles of light) hit the phototransistor, the transistor – and with it the LED — is effectively switched off. When a diminished number or no photons hit the phototransistor, current freely passes through the transistor’s collector-emitter junction, lighting up the LED.


### homework link：

https://www.tinkercad.com/things/i0Zs0F1QmHS-week03lab03/editel
![image](https://github.com/mylin04202/img/blob/main/W03L03.jpg)

## Lab 03b: Touch Sensor (KIT ONLY) 

Using the circuit in the slides, make the touch sensor.
Take a short video to submit of the working circuit and put it on your blog. 



## Lab 04: Feedback systems

### requirement：

Before doing this lab, it's important to do this week's reading, listed below. You may end up doing this lab as homework.

Systems which feedback on themselves often feel more alive to us than static systems which only output data. Design a system, based on what we have learned so far, which feedbacks on itself. How could interaction work within a system which is continually feeding back on itself?

##### homework link：

https://www.tinkercad.com/things/2gEmtTSgQDb-week03lab04/editel
![image](https://github.com/mylin04202/img/blob/main/W03L04.jpg)
