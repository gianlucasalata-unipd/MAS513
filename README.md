# MAS513-Advanced Robotics project

This paper addresses the application of a non contact sensor for the detection of rolling-element bearing damage in induction machines; in particular using a Radar to detect vibrations of motor's shaft.

## Experimental  Hardware

### Vibration Simulator( DyLab MVS-510)

The simulator is composed by a Siemens 2 polar couples induction motor (1) driven by a variable frequency drive (2) and connected to a main shaft which is anchored to the base through multiple bearings (4). For each shaft mounts are present 3 bearing slots but only the central one is the working one. 2 healthy bearings, 1 outer race defected  and 1 inner race defected bearing are available; swapping these bearings in the central positiion of the mounts is possible to simualte every working condition, for example: healthy bearings, only 1 defected or shaft with multple defects. 

A magnetic brake (3), working as a load, is coupled to the main shaft through a reduction gearbox.

In order to measure the vibration of the shaft using a radar, which is characterized by a low resolution (approx. 1mm), the target is located on the right end where the oscillations are higher beacuse is and free end without constraints.

  ![Alt text](/img/vibration_simulator.png?raw=true)

### Radar and Caputer Card(TI-AWR1843+TI-DCA1000EVM)
 ![Alt text](/img/radar.jpg?raw=true)

 --------

# Procedure

The experimental setup require that the radar is located perpendicular to the ground and point straight to the target as shown un the figure below:

 ![Alt text](/img/experimental_setup.png?raw=true)

 Is recommended to cover all the enviroment parts that  are close to the target which  can easily reflect the radio waves; as noticeble in the prevoius image the background is covered with cardoboard in order to reduce the reflection and also all the front part are covered with some paper creating an ideal "tunnel" that should guide the radar to the target (turn off the lights is suggested). All this procedures are to reduce the reflection so reducing the noise in the radar measurements.
## Steps

Follow all the steps described below to replicate the experiment:
- Put in the central slot of the shaft's mounts the bearings you want to use. The defective bearings are marked with: **I** if there is defect in the inner race, **O** if there is a defect in the outer race
- Connect the powersupply to the simulator
- Press the button _Power_ to active the VFD and the control panel turns on
- In order  to set the rotational speed of the shaft: from the VFD control panel, press the button _mode_ until a **F** appear on the screen and using the knob set the frequency. **ATTENTION**: The value on the screen is the supplying voltage frequncy in Hz, the corresponded rotational speed of the shaft is: omega=(60*F)/2;
- Press the button _motor run/stop_ to start up the motor. For safety reasons the plexiglass enclosure must be closed; this safety can be bypassed pressing the electrical switch located behind the motor for the entire run.
- 

