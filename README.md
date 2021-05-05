# Deep Pool Learning
#### Building AI course project
#### Life & Energy saving AI based system for swimming pools

## Summary

“Deep Pool Learning” is Life & Energy saving embedded system, based on AI/DeepLearning computer science methods for public pools, private pools and beyond. This is 24 hours running, standalone system, that can be installed on any pool in the world, providing safe and relaxed environment for all users and in the same time saving energy and making healthier pools. It runs on two separate Convolutional Neural Network based image processing programs and the main program. Deep Pool Learning main program will activate set of alarms, calculate users count and learn to optimally operate filtration system. Alarm can be cell phone massage, audible, light or any other mean of alarming.


## Background

System is intended to be used by pool owners, parents, managers, pool attendants and pool maintenance technicians. It promotes pool safety and healthier environment. For managers and pool owners it provides significant savings and increases pool value in general. For pool attendants and private pool owners it provides more relaxed and safer environment to work and live in. Specially for parents, it triggers an alarm if kids or pets fall in to the pool while they are not attending. For pool technicians it provides less maintenance requirement, more reliable chemical balance and  healthier pools in general, where in the same time helps to comply with local rules and regulations requirements, such as USPH or other.

Deep Pool Learning system is used to:
* Save lives
* Save energy 
* Provide healthier pools
* Provide relaxed environment
* Promote AI based technologies
* Promote Green future solutions
* Stabilize pool chemical balance
* Save filtration and heating  equipment
* Save on operational costs in general
* Reduce pool treatment chemicals consumption
* Help to comply with local rules and regulations
* Help to monitor social distancing in the pools
* Be an adoptable system to comply with future operational changes   


## How the system works?

### Deep Pool Learning as software solution for modern pools
Two separate Neural Network based programs are running in real time. 
With first program, that was previously trained, photos of the pool ledges are taken and processed to calculate the count of the pool users. The count is program output that will be used for cross-check with second program, to signal the first alarm, and to operate pool filtration equipment accordingly.
Second program is processing photos of total pool area and calculating its own count that will be cross-check with first program, and is trained to directly recognize potential drowning that will trigger another/different set of alarms.

Idea is based on the fact that everyone needs to get inside and out of the pool from its ledge. This can be used as a big advantage in programming/training the pool software and system technology. In this way it will be easier to count the number of the persons using the pool at any moment do the cross-check count for entire pool area surface in real time, thus recognizing the total count of user and recognizing any mismatch. 

When camera/s of the first program takes the photo and is procseesed in our NN, in case of discrepancy between the count of the two running programs timer is initiatetd that will set off the alarm if exceeded. Othervised that photo is deleted, followed by a new photo and the same count and the same process.
SImilar logic is following the second NN that is trained to recognise actual drowning and obtain separate count. Accordingly, it deletes photo and continues to process a new photo if nothing is unusual.

Complete program, consisted of two NNs can be represented in these logic steps:
   * 1.	First camera/s takes a photo of the ledge area
   * 2.	Run the photo through first Neural Network
   * 3.	Output the users count. Value "X"
      * 3a. Send the value "X" to embedded system (PLC or MicroController)
   * 4.	Second camera takes a photo of pool surface
   * 5.	Output the second count. Value "Y"
   	  * 5a. Output alarm if NN recognise drowning
      * 5b. Save photos in dedicated memory
   * 6.	Do the cross-check calculation X-Y. Value "sum"
   * 7.	If sum =! 0:
      * 7a.	Trigger pre-set timer count
      * 7b.	Trigger alarm after timer runs out
      * 7c.	Save photos in dedicated memory
   *8.	If sum == 0:
      * 8a.	Delete the photos
   *9.	Repeat the process from the beginning

Additionally, there can be a submerged water cameras on the bottom or cameras behind side glass where applicable.

### What is bather load, chemical balance and how the conventional pool systems work?
Bather load is nothing but the maximum number of the people that can use the pool in the same time. In our program, bather load will be the same as the value "X" or "Y". Bather load is tightly related with the quality of the pool water and is given by the Departments of Health or similar institutions. For example, for Cruise Ship pools, USPH is the regulatory body that states in its VSP manual that flow of the water through filtration system must be 5 gallons per minute for every person. With that information we can write simple formula to calculate Bather Load for any specific pool:

BL = Water Flow Through Filtration System / 5 

Filtration pump flow in gal/min divided by 5 will give us the Bather Load number (integer). 

Conventional pools are running with filtration pump on maximum power rate at all time, which cannot be insurance to avoid the flow drop if filters get dirty. So, the BL is pre-calculated value that can change in time, which means for safety it will be lower than the actual maximum capacity of our filtration system. This is where Deep Pool Learning comes to rescue.
From this point of view, we can see that if we know at all time how many people are using the pool and what is required flow of the of our filtration equipment at that moment, we can more successfully and reliably run our system. When the pool is not as crowdy, we can reduce speed of filtration scientifically and save energy even more. Especially during the nights or weekends, since pool equipment is nonstop running at all time even if pools are closed. 
Closely connected to the flow of the filtration system is regulation of Chemical Balance of the pool. In short, it means that by knowing number of users and the flow we can obtain smoother curve of the pool chemical values (pH, Cl, Br, etc.) and not overdose the pool. In time we can have a AI program to learn the optimal solutions at all time.

### Deep Pool AI
So we can say that our AI program can learn to run the pool system efficiently and reliably just by knowing the BL (count, value "X" obtained in step 3.), pumps flow and values of the Cl an pH.


<img src="https://www.wowamazing.com/wp-content/uploads/2015/08/ce95100000000000.jpg" width="400">


```
# Program writen below is a general idea of the DeepPoolLearning python program.
# Two CNN running separatly are procesing images from two cameras in real time
# and are returning users count. Secon CNN additionaly recognises possible actual drowning.
# Main program calculates differenace between two information, gives output to Inverters and outputs alarms.

import numpy as np
import RPi.GPIO as GPIO
import time

def main(X, Y, Z):
   sum = X - Y
   if sum != 0:
      return Alarm_Out(1)
   if Z is true:
      return Alarm_Out(1)  
   return Inverter_Out(X)   

def pool_ledge(image1):
   # process first image through forward propagation of first Convolutional Neural Network
   # and return users count (people in the pool)
   return X
   
def pool_area(image2):
   # process second image through forward propagation of second Convolutional Neural Network
   # and return users count as value Y (people in the pool)
   # and returns value Z if CNN recognises drowning inside pool area image
   
   return Y 
   return Z
   
def Inverter_Out(value):
   # Define analog output on the Raspery Pi
   # Analog out is matching count of pool users obtained by CNN
   # And operates Filtration system inverters accordingly
   
   out_pin = 18
   GPIO.setmode(GPIO.BCM)
   GPIO.setup(out_pin, GPIO.OUT)  
   pwm_out = GPIO.PWM(out_pin, 500)
   pwm_out.start(value)
   
def Alarm_Out(alarm):
   # Takes as input alarm values from main program
   # Outputs alarm on one of the Raspbery pins as digital output
   
   alarm_pin = 15
   GPIO.setmode(GPIO.BCM)
   GPIO.setup(alarm_pin, GPIO.OUT)
   if alarm == 1:
      GPIO.output(alarm_pin1, True)
   else:
      GPIO.output(alarm_pin1, False)
      
main(X, Y, Z)
```

## Challenges

Since we are dealing with life safety of humans or pets, challenging will be to get system to be reliable and trustworthy. It will still need an attendant on site, to be connected in some way with system alarms and to be a first person in quick response team.

## What next?

It could be extended to public beach areas and beyond. As we increase ability to collect larger amount of data and process it, larger areas of monitoring may be implemented.
With wright programmers, engineers and enthusiasts, project can only grow and be extended in many ways, and most importantly promote AI technologies. It can have a great impact on the future of AI and gain further developments on other AI fields as well. It will be a challenge to get it working perfectly and reliably, but the revard for accomplishment is priceless. Imagine at the entrance of any public pool sign “This pool is protected by AI technologies” and AI being advertised for being responsible for having safest and healthiest pools in the world.


## Acknowledgments

Special thanks' to University of Helsinky and Reaktor for setting up their inspirational courses "Elements of AI" and "Building AI". https://buildingai.elementsofai.com
* do not use code, images, data etc. from others without permission
* when you have permission to use other people's materials, always mention the original creator and the open source / Creative Commons licence they've used
  <br>For example: [Sleeping Cat on Her Back by Umberto Salvagnin](https://commons.wikimedia.org/wiki/File:Sleeping_cat_on_her_back.jpg#filelinks) / [CC BY 2.0](https://creativecommons.org/licenses/by/2.0)
