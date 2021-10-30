# MAS513-Advanced Robotics project
This paper addresses the application of a non contact sensor for the detection of rolling-element bearing damage in induction machines; in particular using a Radar to detect vibrations of motor's shaft.

## Experimental Setup Hardware
### Vibration Simulator( DyLab MVS-510)
The simulator is composed by a Siemens 2 polar couples induction motor (1) driven by a variable frequency drive (2) and connected to a main shaft which is anchored to the base through multiple bearings (4). For each shaft mounts are present 3 bearing slots but only the central one is the working one. 2 healthy bearings, 1 outer race defected  and 1 inner race defected bearing are available; swapping these bearings in the central positiion of the mounts is possible to simualte every working condition, for example: healthy bearings, only 1 defected or shaft with multple defects. 
A magnetic brake (3), working as a load, is coupled to the main shaft through a reduction gearbox.
In order to measure the vibration of the shaft using a radar, which is characterized by a low resolution (approx. 1mm), the target is located on the right end where the oscillations are higher beacuse is and free end without constraints.

  ![Alt text](/img/vibration_simulator.png?raw=true)
### Radar and Caputer Card(TI-AWR1843+TI-DCA1000EVM)
--------
 ![Alt text](/img/radar.jpg?raw=true)
## Steps
Follow all the steps described below to replicate the experiment


Gianluca Salata
