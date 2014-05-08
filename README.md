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

In order to implement this design, some changes were made to the MIPS Processor.  



##Diagram
Below is the original design.  Outlined in red are the portions that were changed.  


![alt tag](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Altered_Schematic.PNG "Altered Controller")


The changes to this section of the schematic can be seen below: 


![alt tag](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Altered_Schematic_2.JPG "Altered Controller")




These changes were made for the following reasons: 

In order for the ori command to work properly, the sign extend cannot be used for negative numbers.  If this were the case, then the first 4 hex digits of the result of the ori function would be "FFFF" if a negative number was used as the immediate value.  Therefore, whenever the ori command is chosen, a zero extend should be performed on the immediate value rather than a sign extend.  





##Tables
The changes can be seen in the tables below: 


///////////////insert ALU decoder



///////////////insert Main decoder




##Code: 




In order to implement these changes into the MIPS design already created, the main decoder and the ALU decoder were edited as required.  Copies of these files can be seen here:  [mips](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Task_3_mips.txt) and [testbench](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Task3_Testbench.txt).  The following changes were made to the code: 



//////////////////insert what changes were made to the code.  




##Code Testing

The following assembly command was then implemented.

```
ori $S3, $S2, x8000
```

Note: 8000 is in decimal, as stated in the lab.  

This command was then converted into binary, as in Task 2, and performed right after the contents of registers $S1 and $S0 were summed.  

This binary code can be seen below.




////////////////insert binary code below
```
```



The binary code was then converted to hex so that it could be used in the program.  




/////////////////////insert bex code below: 








This program was then run and tested, just like in Task 2 step 2 shown above.  

A screenshot of this test can be seen below: 



//////////////////////////insert picture of task 3 simulation 
![alt tag](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Task_3_Simulation.PNG "Task 3 Simulation")




#Documentation: 
C3C Sabin Park helped me figure out how to add the correct waveforms to the simulation.  
