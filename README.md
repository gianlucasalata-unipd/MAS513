# MAS513-Advanced Robotics project

This paper addresses the application of a non contact sensor for the detection of rolling-element bearing damage in induction machines; in particular using a Radar to detect vibrations of motor's shaft. The complete description of the expriment with the anlayss of the data can be found: 
[here](https://github.com/gianlucasalata-unipd/MAS513-Continuous_motors_health_monitoring/blob/main/Third_assignment.pdf)

## Experimental  Hardware

### Vibration Simulator( DyLab MVS-510)

The simulator is composed by a Siemens 2 polar couples induction motor (1) driven by a variable frequency drive (2) and connected to a main shaft which is anchored to the base through multiple bearings (4). For each shaft mounts are present 3 bearing slots but only the central one is the working one. 2 healthy bearings, 1 outer race defected  and 1 inner race defected bearing are available; swapping these bearings in the central position of the mounts is possible to simulate every working condition, for example: healthy bearings, only 1 defected or motor with multple defects. 

A magnetic brake (3), working as a load, is coupled to the main shaft through a reduction gearbox.

In order to measure the vibration of the shaft using a radar, which is characterized by a low resolution (approx. 1mm), the target is located on the right end where the oscillations are higher beacuse is and free end without constraints.

  ![Alt text](/img/vibration_simulator.png?raw=true)

### Radar and Caputer Card(TI-AWR1843+TI-DCA1000EVM)
The AWR1843 single-chip is used. This radar is a CWFM one (continuous wave frequency modulation) based on mmW (millimeter wave) technology that uses short-wavelength electromagnetic waves so in the millimetre range; this means working in a frequency range  of 30-300 GHz. 
 It is based on the fundamental concept of the transmission of an electromagnetic signal, which interferes with an object in its path and then gets reflected back.The electromagnetic signal sent by the radar its called \textit{chirp},generated by synthesizer, it is a sinusoid whose frequency increases linearly with time. A transmitter antenna (TX ant) emits the chirp, and the reflection of this chirp gets captured by the receive antenna (RX ant). These 2 signals get combined in a “\textit{mixer}”, to produce an intermediate frequency (IF) signal. 
if there are multiple objects  in front of the radar, the IF signal then consists of multiple tones, and each tone is proportional to the range of each object. This signal then gets digitalized, and an FFT (fast Fourier transform) is performed on it. In the resulting frequency signal, called range FFT, the location of the peaks corresponds to the range of the objects.
To acquire data and set parameters, the radar is used with the acquisition card, DCA1000EVM which  enables the user access to the sensor’s raw data over Ethernet.
The entire setup require 2 power supply with at least 2.5[A] with barrel connector (2.1[mm]) one for each board and for the radar itself a micro-usb cable is used to connect it to a laptop. The acquisition card requires micro-USB cable and RJ45 Ethernet cable to connect it to the laptop and a 60pin Samtec cable which connect this board to the radar.
 ![Alt text](/img/radar.jpg?raw=true)

 --------

# Procedure

The experimental setup require that the radar is located perpendicular to the ground and point straight to the target as shown un the figure below:

 ![Alt text](/img/experimental_setup.png?raw=true)

 Is recommended to cover all the enviroment parts that  are close to the target which  can easily reflect the radio waves; as noticeble in the prevoius image the background is covered with cardoboard in order to reduce the reflection and also all the front part are covered with some paper creating an ideal "tunnel" that should guide the radar to the target (turn off the lights is suggested). All this procedures are to reduce the reflection so reducing the noise in the radar measurements.
## Guides

Follow all the steps described below to set up the vibration simulator
- Put in the central slot of the shaft's mounts the bearings you want to use. The defective bearings are marked with: **I** if there is defect in the inner race, **O** if there is a defect in the outer race
- Connect the powersupply to the simulator
- Press the button _Power_ to active the VFD and the control panel turns on
- In order  to set the rotational speed of the shaft: from the VFD control panel, press the button _mode_ until a **F** appear on the screen and using the knob set the frequency. **ATTENTION**: The value on the screen is the supplying voltage frequncy in Hz, the corresponded rotational speed of the shaft is: omega=(60*F)/2;
 ![Alt text](/img/VFD.png?raw=true)
- Press the button _motor run/stop_ to start up the motor. For safety reasons the plexiglass enclosure must be closed; this safety can be bypassed pressing the electrical switch located behind the motor for the entire motor's run.

To capture the radar data, the following hardware is required:
-	AWR1843, 5V / >2.5A power supply, micro-USB cable.
- DVA1000EVM, 5V / >2A power supply, micro-USB cable, RJ45 ethernet cable, 60pin Samtec cable.

And this software:
-	mmWave Studio (Version 2.1.1.0 will be used ).
-	Matlab Runtime Engine v8.5.1 32bit.
-	Code Composer Studio > v7.1 or CDS Emulation Software Package v6.0.579.0 or higher


Follow all the steps described below to set up the radar:
-  set to development mode on the board obtainable with the switches configuration shown in the figure below:
 ![Alt text](/img/switches.png?raw=true)
- check the port number in which the board and the radar are connected, as shown below ( in this case are port number 3 and 4):
![Alt text](/img/ports.png?raw=true)
- The FTDI device ports of the DCA1000 board however won’t be available because their driver is not installed. The driver for these ports can be found in the mmWave Studio folder.
- Connect thr Ethernet cable of the DCA1000  to the computer and in the local area network properties a static IPv4 address of 192.168.33.30 and a subnet mask of 255.255.255.0 need to be set.
- Run the mmWaveStudio software
-  Ensure that DCA1000 is selected.
- Press “Set” in Reset control.
- Select the right COM port number based on figure above and a Baud Rate of 115200 and connect.
- Load the appropriate BSS (radarss.bin)
- Load MSS firmware (Masterss.bin); The binary is based on the device variant being used (1243/1443/1642) and the silicon PG version being used (ES1.0, ES2.0, ES3.0).
- Click the SPI Connect button.
- Click the RF Power up button.
 ![Alt text](/img/radar1.png?raw=true)
 
 Now all connection are establish and this appear on the software:
  ![Alt text](/img/status.png?raw=true)
- Move to "Radar Studio Static config" tab
- Select the desired TX and RX channels,in ADC Config select the desired AD configuration and click Set.
- Click the Set button in the Advanced Configuration box.
- In the LP mode box select "Regular ADC".
- Press "RF Init Done" button.
    ![Alt text](/img/radar2.png?raw=true)
- Move to "DataConfig" tab.
- Clic Set button in the "data path config" box.    
- Choose a 600[Mbps] clock rate and click.
- Select the 4 LVDS lanes and click Set.
![Alt text](/img/radar3.png?raw=true)
- Move to "Sensorconfig" tab.
- Define the FMCW chirp profile  and click Set.
- Select the chirp configuration and click Set.
- Select the frame configuration and click Set.
-  Select the Dump file pathname in which the radar data will be saved and click Set.
![Alt text](/img/radar4.png?raw=true)
- Click on  "SetUp DCA1000" on the left side of teh pannel
- In the pop up window click "Connect, Reset and configure"
To start the acquisition press in order:
- "DCA1000 ARM"
- "Trigger Frame"
- "Post Proc"
- ![Alt text](/img/radar5.png?raw=true)
