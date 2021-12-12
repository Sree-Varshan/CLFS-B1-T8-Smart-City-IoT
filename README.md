# CLFS-B1-T8-Smart-City-IoT
Smart Cities bring Internet of Things to life with seamless connectivity that improves overall quality of life, promotes econimic growth, increases sustainability and managing of resources. It is more than just a vision. A "Smart City" is an urban area that incorporates information and communication technologies into its systems. Sensors gather data to inform authorities and residents, reducing waste and making resource consumption more efficeint.

This is a capstone project done as part of Careerlabs Finishing School.

The project focuses on 4 main areas that must be in a city:

Traffic Control System
Automatic Parking System
Smart Home
Enviromental Monitoring

## Traffic Control System

This project has been divided into 4 phases:
* Automatic street light system
* Have a 4 way traffic control system.
* The ambulances will send a signal to the aws cloud iot topic and raspberry pi will make that
lane as green and other lanes as red.
* Show the status of traffic lights on a dashboard (Thingspeak)

### Phase 1: Automated Street Lighting System
Smart Street light is a robotized framework which automate the road. The primary point of Smart Street light is to reduce the power utilization. The Smart road light will turn to be ON when there is not enough sunlight for travelling and about generally the lights will be turned OFF when ther is enough sunlight. With improvement in technology, things are getting to be easier and simpler for everybody around the world today. This is just a demo version of the system.

Components used in this part of the project are:

Raspberry Pi 4
LED
LDR sensor
jumper wires
a resistor and a capacitor

https://user-images.githubusercontent.com/95992947/145700866-6e6be97f-a5d9-4bdb-b53d-1d76bf97187c.mp4

* Python Script for Street Light System

import RPi.GPIO as GPIO
import time
GPIO.setmode(GPIO.BOARD)
delayt = .1
value = 0
ldr = 7
led = 11
GPIO.setup(led,GPIO.OUT)
GPIO.output(led,False)
def rc_time(ldr):
	count = 0
	GPIO.setup(ldr,GPIO.OUT)
	GPIO.output(ldr, False)
	time.sleep(delayt)

	GPIO.setup(ldr,GPIO.IN)

	while(GPIO.input(ldr) == 0):
		count+=1

	return count

try:

	while True:
		print("Ldr Value:")
		value = rc_time(ldr)
		print(value)
		if(value>=200000):
			print("Lights are ON")
			GPIO.output(led,True)
		if(value<200000):
			print("Lights are OFF")
			GPIO.output(led, False)
except KeyboardInterrupt:
	pass

finally:
	GPIO.cleanup()
