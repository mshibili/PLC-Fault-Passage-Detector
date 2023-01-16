# PLC-Fault-Passage-Detector
Power-Line Communication enabled Fault-Passage Detector for High-Volt Lines.


##Power Line Faults

Faults can occur due to various reasons. Broadly we can categorize faults
into two,
###a. Line-Earth Faults:
High volt electricity leaking to earth due to insulator punctures, broken lines, or nearby trees and buildings. As the metallic body of any electrical
equipment or device is connected to the earth.

###b. Line-Line faults:
Short circuit in between the lines due to various environmental or manmade causes. A line to line fault or unsymmetrical fault occurs when two conductors
are short circuited. In the figure shown below shows a three phase system with a line-to-line fault phases b and c. The fault impedance is assumed to be Zf.
The LL fault is placed between lines b and c so that the fault be symmetrical with respect to the reference phase a which is in-faulted.

## Conventional Power-Line Fault Rectification Procedure
In practical electricity, people use the trial and error method to detect the fault location (Line to line fault / line to ground fault) of a transmission line.
They feed supply at the single end at a time by dividing that transmission line into two parts and check the fault up to that section. These processes go on until
they find the fault area. After checking if they found anything, then it is ok to go forward.This process is done from both ends and they sort out the exact
location. For finding out the fault phase, they use megger (check the value of resistance between the line to ground and Line to Line for each phase). These
technologies take more human effort and consume more time.

## How Fault Passage detector Function

FPD's are designed to measure the line current from Electromagnetic field around power-line conductor. A coil present in the EM field of power-line can be used to measure the current flow based on the transformer equation. This kind of coils are called current transformers.
Consider a CT coil with a turn ratio 20/0.01 = 2000
ie,
If primary (Power-line) has 20Amp current flow CT induces 10milli-Amps of current flow across burden resister.
Power-line Current(Ip) = Coil_current(Is) x CT_ratio (2000)
Thus, by measuring the coil current we can calculate the current present in the power-line using CT ratio. 
To measure the coil current (Is), we use shunt/burden resister method. Here the Burden resistance is 20 Ohms.
Using ohms law,
Coil-current = Voltage-drop(Vshunt) x Resistance(Rshunt)
Microcontroller ADC trace the voltage across the resistance to calculate Coil_current and Power line current. 
If the Power line current exeeds the maximum load value the occurance considered to be a fault.

## Power Line communication
The data transmission in the power line
can be done various methods and protocols. The signal to be transmitted is modulated to FM analog signal. The digital one value is represented by the
high-frequency components and the digital low value is converted to low-frequency components. Both frequencies are at the range of Kilo Hz
(varying for protocols and methods from 10KHz to 130 kHz ). The frequency switching technique is also called FSK (Frequency shift keying) since the
digital signal is transmitted through the discrete of the carrier signal. The frequency changed modulated signal then coupled with the AC power line via
‘High pass filters’ which reject the low frequency 50Hz AC signal and make the wire available for the transmission of data. When multiple devices are
interconnected in the PLC network, we use the multiplexing technique called FDM.This method allows simultaneous data transfer on the available frequency range. FDM assigns frequency divisions for each device to enable multiplexing.

Digital data consist of start code, letter code, and number code. The start code will poke the receiver and make it ready to read the data. The letter code consist of transmitting device address and number code enclose the data. Further for more application parameters, the data sequence can be extended. Here we use the following data sequence for efficient AMR and power theft detection.

● Start Code = 4 bits
● House code = 4 bits
● Extended code 1 = 5 bits (01111)
● Unit code (device code) = 4 bits
● Data = 8 bits
● Command = 8 bits


