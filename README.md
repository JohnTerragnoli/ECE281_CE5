ECE281_CE5
==========


#**Task 1**
The purpose of this task was to initialize the registers $S0 and $S1 with the decimal values 44 and -37 respectively.  To add and store the result in $S2.  Then, this value at $S2 will be stored at the hexadecimal memory address x54.  The MIPS code below performs the desired actions: 


Task 1 Code: 
```
addi $S0, $0, 44
addi $S1, $0, -37
add $S2, $S0, $S1
sw $S2, 0x54($0)
```



#**Task 2** 

For this portion of the computer exereise the instructions made in task 1 were hand assembled.  The machine code was then written in hexidecimal.  This process can be seen below: 

Task 2 Code:

Assembly Code:
```
addi $S0, $0, 44
addi $S1, $0, -37
add $S2, $S0, $S1
sw $S2, 0x54($0)
```


Converted to Decimal:

Always switch rt and rs.  Therefore, $s0 and $0 are switched when convertinging into decimal.  
```
--------------
|8|0|16|44|
------------
|8|0|17|-37|
---------------
|0|16|17|18|0|32|
---------------
|43|0|18|84|
-------------
```



Converted to Binary:

```
0010 0001 0001 0000 0000 0000 0010 1100
0010 0000 0001 0001 1111 1111 1101 1011
0000 0010 0001 0001 1001 0000 0010 0000
1010 1100 0001 0010 0000 0000 0101 0100
```


Convert into Hex: 

```
0x2010002C
0x2011FFDB
0x02119020
0xAC120054
```

This hex code was then copied into the ISE Project Navigator.  This [mips.vhd](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/mips.vhd) file and this [Task_2_testbench](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Task_2_Testbench.vhd)  were used to run the code.  The actual code was copied into the testbench file and the mips.vhd file was not changed.  Once the simulation was initiated, this [file](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/mips_waveform.wcfg) was loaded into the simulator so that it would work correctly.  



#Simulation Snapshot 

The waveform file given in the lab did no run correctly.  So in order to get the simulation to show the desired waveforms, the waveforms had to be selected in the "Instance and Process" section of the simulator.  They were added manually.  This simulation can be seen below: 

![alt tag](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Task_2_Simulation.PNG "Task 2 simulation")

After the correct waveforms were added, a waveform file was created and saved, so that it could be refereced for later work.  This is the [New_Waveform](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/actual_waveform.wcfg) file.  


#Task 3: 

The purpose of this task was to add the instruction "ori" to the MIPS design.  The ori command means to take a value in from memory and "or" this value with an immediate number.  

In order to implement this design, some changes were made to the MIPS Processor.  These changes can be seen below: 




////////////insert picture of altered MIPS design.  






##Diagram
These changes were made for the following reasons: 



////////////insert reasons why the changes were made




##Tables
The changes can be seen in the tables below: 


///////////////insert ALU decoder



///////////////insert Main decoder




##Code: 




In order to implement these changes into the MIPS design already created, the main decoder and the ALU decoder were edited as required.  The following changes were made to the code: 



//////////////////insert what changes were made to the code.  




##Code Testing


#Documentation: 
C3C Sabin Park helped me figure out how to add the correct waveforms to the simulation.  
