# Raspberry-pi-ultrasonic-live-data-to-phone-as-message-using-Node-Red
Ultrasonic sensor is connected to the raspberry pi . These sensor values are collected in our mobile in form of messages.
This is done using Node Red.
## Node Red
[Node-RED](http://nodered.org/) is a programming tool for wiring together hardware devices, APIs and online services in new and interesting ways.

It provides a browser-based editor that makes it easy to wire together flows using the wide range of nodes in the palette that can be deployed to its runtime in a single-click.It is build on node.js.



## Installation of Node Red on raspberry pi


[installation process](http://nodered.org/docs/hardware/raspberrypi)
## Node Red on raspberry pi
  Node Red is defaultly installed in  Raspbian Jessie operating system.Type the command node-red-start in the terminal.Once the node red 
  is started, point a browser at the local host which is provided.
  ![node red start](https://cloud.githubusercontent.com/assets/25893079/26528802/8a7e8fba-43d0-11e7-8e1f-d7a3de0c2402.png)
  once the Node Red is started in the browser , connect the following nodes shown below
  
![node red flow](https://cloud.githubusercontent.com/assets/25893079/26528548/6dfa1bba-43cc-11e7-8717-66799d9270a1.png)
## Creating a Twilio account
  [Twilio] (https://www.twilio.com)is a Cloud communications platform for building SMS, Voice & Messaging applications on an API built for global scale. 
  
  
  Fill all the credentials , token number  and the phone number which is provied.
  ![add credentials in twilio](https://cloud.githubusercontent.com/assets/25893079/26528553/81af1804-43cc-11e7-8a5c-cb8df6f89983.png)
  Add the mobile number for which you need to get the message

![twilio](https://cloud.githubusercontent.com/assets/25893079/26528549/748334b2-43cc-11e7-8104-485d40f52e90.png)
### Create a python file and copy the code.
import RPi.GPIO as GPIO

import time

GPIO.setmode(GPIO.BCM)

TRIG = 23
ECHO = 24

print "Distance Measurement In Progress"

GPIO.setup(TRIG,GPIO.OUT)
GPIO.setup(ECHO,GPIO.IN)

GPIO.output(TRIG, False)
print "Waiting For Sensor To Settle"
time.sleep(2)

GPIO.output(TRIG, True)
time.sleep(0.00001)
GPIO.output(TRIG, False)

while GPIO.input(ECHO)==0:
  pulse_start = time.time()

while GPIO.input(ECHO)==1:
  pulse_end = time.time()

pulse_duration = pulse_end - pulse_start

distance = pulse_duration * 17150

distance = round(distance, 2)

print "Distance:",distance,"cm"

GPIO.cleanup()




  In the exec node write the command sudo python followed by path of the code created.

![execution of exec node](https://cloud.githubusercontent.com/assets/25893079/26528557/88c006bc-43cc-11e7-8fe3-07483f04a54a.png)
Finally connect all the node and deploy the application.Finally data will be received to your mobile as message.
![mobile message](https://cloud.githubusercontent.com/assets/25893079/26528810/c1b59a82-43d0-11e7-855c-d610b92b6d66.png)




