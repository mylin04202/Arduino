


## Lab 01: PCBs

#### Requirement：

Watch the video and do either the Eagle or KiCad tutorials. PCBs are circuit boards
Learn to use Eagle

Protip: If you use your student email and register as a student with Autodesk, it will unlock a large amount of free software, including a less limited version of Eagle. Also Maya is free.

#### Project：

![image](https://github.com/mylin04202/img/blob/main/image-20201215210708325.png)



## Lab 02: Learn the sensors of the Arduino Nano 33 Sense BLE

#### Requirement：

[The Arduino Documentation](https://www.arduino.cc/en/Guide/NANO33BLESense)[The IMU](https://www.arduino.cc/en/Reference/ArduinoLSM9DS1)

Note, you'll be able to find Arduino libraries for every sensor on the chip. Just google the part. The data sheets are linked. Any library will come with basic code samples to get you going. Try a few out on your own. It's simple.



#### Project：

![image](https://github.com/mylin04202/img/blob/main/image-20201215213913619.png)

![image](https://github.com/mylin04202/img/blob/main/image-20201215213817509.png)

![image](https://github.com/mylin04202/img/blob/main/image-20201215213901546.png)

![image](https://github.com/mylin04202/img/blob/main/image-20201215213851801.png)



## Lab 03: Interfaces in the future library

#### Requirement：

Create a fictional interface which would exist in your library of the future using the Arduino Nano 33 Sense. It can be anything, but it must fit within the fictional world you created. Tell a very short continuation of your story along side the lab's project log.

#### Ideas💡:

![img](https://www.yiboard.com/data/attachment/forum/201911/24/105844ua7wk8827es74ooo.jpg)

| **Sensor name**       | **Description**                           |
| --------------------- | ----------------------------------------- |
| [LSM9DSI – ST]        | Accelerometers, gyroscopes, magnetometers |
| LPS22HB – ST          | Manometers                                |
| HTS221 – ST           | Temperature and humidity sensors          |
| APDS9960 – Avago Tech | Proximity, light, colour, gesture         |
| [MP34DT05 – ST]       | Microphone                                |



Because my library of the future is more inclined to use **biotechnology and quantum technology**. So I would like to use the nano 33 ble in my library to **assist people with disabilities.**

For example, for the visually impaired, perhaps I could use the **MP34DT05-ST** sensor to get signals to activate and use other devices in the library, meaning that many of the functions in my library of the future could be **voice-activated.** For people with physical and hearing disabilities, I would like to use the **APDS9960 - Avago Tech sensor** for the gesture input part. So there may be a preference for **using the sensor for signal input in the controls.**



### <u>Examples used for reference</u>

#### 01. Voice-controlled  Robotic Arm

Perhaps the robotic arm in the library can be controlled by **voice control（MP34DT05-ST** ）for disabled people

![一种声控机械臂的制作方法](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRJztZexGfodKWOI1pPfTL9T4iG_2bG8TkWLQ&usqp=CAU)



#### 02. Visually guided brain-voice controlled assistive robot for people with disabilities

##### Three components: 

machinery, information acquisition and control

##### Features: 

information acquisition section with brainwave acquisition sensors for brainwave signals, CCD cameras for visual signals and microphones for sound signals

##### The control section:

 the EEG, visual and audio signals are evaluated and the corresponding operations are performed

##### Diagram of the control principle：

![image](https://github.com/mylin04202/img/blob/main/image-20201215085439514.png)
