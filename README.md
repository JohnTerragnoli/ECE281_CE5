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

Always switch rt and rs when converting the command into machine language.  Therefore, $s0 and $0 are switched when convertinging into decimal. 

```
--------------
|8|0|16|44| #put 44 in the register $S0
------------
|8|0|17|-37|  #put -37 in the register $S1
---------------
|0|16|17|18|0|32|   #adds the values in $S0 and $S1 and stores the result in $S2.  
---------------
|43|0|18|84|  #stores the value in the $S2 register and saves it in memory address x54.  
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

The waveform file given in the lab did no run correctly, unless the name of the testbench was changed to a specific string.  So in order to get the simulation to show the desired waveforms, the waveforms had to be selected in the "Instance and Process" section of the simulator.  They were added manually.  This simulation can be seen below: 

![alt tag](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Task_2_Simulation.PNG "Task 2 simulation")

After the correct waveforms were added, a waveform file was created and saved, so that it could be refereced for later work.  This is the [New_Waveform](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/actual_waveform.wcfg) file. 


To assure that the program was implemented correctly, the signal ALUout was analyzed.  For the first clock cycle, the value 44 appeared as the ALUout.  This makes sense because the actual operation that is occuring is storing the value of 44 + 0 into register $S0.  To do this the ALU is required.  This same technique was used for the second isntruction.  The next clock cycle the signal was -37, corresponding to the second instruction.  For the next clock cycle, the ALUout was the sum of those numbers.  That was the third instruction.  For the next clock cycle after that, the memwrite signal changed to 7, meaning that the signal with a value of 7 is being written into memory.  All of these steps represent the tasks that the program was supposed to accomplish.  




#Task 3: 

The purpose of this task was to add the instruction "ori" to the MIPS design.  The ori command means to take a value from a register and "or" this value with an immediate number.  

In order to implement this design, some changes were made to the MIPS Processor.  



##Diagram
Below is the original design.  Outlined in red are the portions that were changed.  


![alt tag](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Altered_Schematic.PNG "Altered Controller")


The changes to this section of the schematic can be seen below.  This is a close-up of the section outlines in red.   


![alt tag](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Altered_Schematic_2.JPG "Altered Controller")




These changes were made for the following reasons: 

In order for the ori command to work properly, the sign extend cannot be used for negative numbers.  If this were the case, then the first 4 hex digits of the result of the ori function would be "FFFF" if a negative number was used as the immediate value.  This means that the result from the ori command would always be wrong.  Therefore, whenever the ori command is chosen, a zero extend should be performed on the immediate value rather than a sign extend.  To decide between this sign extend and the zero extend, a multiplexer was built.  Then an extra bit was added to the ALUsrc command, so that the controller can command whether to use the zero extend or the sign extend when it is necessary.  




##Tables
The changes can be seen in the tables below: 


Below is the ALU decoder

| ALUOp 1:0 | Meaning |
|---|---|
| 00 | Add |
| 01 | Subtract |
| 10 | look at function field |
| 11 | ori |


The last line was the only part of this table changed from the instructions in the lab.  The 11 space was left blank, so this command was seized and used for the ori command; it could have been programed for anything.  
 

Then the table for the Main Decoder was built.  This can be seen below: 

| Instruction | (Op(5:0) | RegWrite | RegDst | AluSrc (1:0) | Branch | MemWrite | MemtoReg | ALUOp(1:0) | Jump | 
|---|---|---|---|---|---|---|---|---|---|
| R-Type | 000000 | 1 | 1 | 00 | 0 | 0 | 0 | 10 | 0 | 
| Lw | 100011 | 1 | 0 | 01 | 0 | 0 | 1 | 00 | 0 | 
| sw | 101011 | 0 | X | 01 | 0 | 1 | X | 00 | 0 | 
| beq | 000100 | 0 | X | 00 | 1 | 0 | X | 01 | 0 | 
| addi | 001000 | 1 | 0 | 01 | 0 | 0 | 0 | 00 | 0 |
| j | 000010 | 0 | X | XX | X | 0 | X | XX | 1 | 
| ori | 001101 | 1 | 0 | 11 | 0 | 0 | 0 | 11 | 0 |


The only line that was created in this line was the last row.  This line was filled out simply by considering what the "ori" command does and what it requires.  

The last row of this table was used to modify the signal that went into the "controls" signal.  




##Code: 




In order to implement these changes into the MIPS design already created, the main decoder and the ALU decoder were edited as required.  Copies of these files can be seen here:  [mips](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Task_3_mips.txt) and [testbench](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Task3_Testbench.txt).  The following changes were made to the code: 

The biggest change was to create, declare, and instantiate a zero extender that was hooked up to the instruction wire.  Then, a wire signal comming out of the extender was declared.  After this was done, another instantiation of the mux2 multplexer was created.  The two inputs were the sign extend and the zero extend, as shown in the schematic above.  This was not difficult.  What was difficult was creating the control signal for this new mux.  The control signal comes form the ALUsrc, as defined in the table above.  In the original mips vhdl design, the ALUscr signal was only one bit long.  To accommodate for the ori command, the ALUsrc signal was lengthened to be 2 bits long.  Doing this, however, had implications as well.  All of the parts that used the ALUsrc signal had to account for this length change.  This was done by changing declarations to be std_logic_vectors instead of just std_logic.  Also, the control signal was lengthened by one bit, because it contains the ALUsrc signal.  

The changes above was the successful idea.  However, multiple unsuccessful methods were tried first.  One of the earliest ideas was to use a new mux that chose between the extend signals.  The control signal would then come right off of the instr wire; the control signal would be 6 bits long, and the zero extend would only be chosen if the ori command was being used.  This design was flawed because the final extend signal was made too soon, and the ori command was never actually used with these results.  This is mostly likely because of the clock cycle.   I decided that using a choser for a multiplexer was a bad idea if the choser did no originate in the control box.  

Another idea was to lengthen the ScrB mux to have 3 inputs.  This could have worked, however, at the time it seemed easier to just create a new instantiation of the 2 bit mux.  Therefore, this idea was quickly abandoned.  



##Code Testing

The following assembly command was then implemented.

```
ori $S3, $S2, x8000 #or's the value stored in register $S2 with the immediate value x8000.  
```

Note: 8000 is in hexadecimal, as stated in the lab.  

This command was then converted into binary, as in Task 2, and performed right after the contents of registers $S1 and $S0 were summed.  

| Op code | rs | rt | imm | 
|-------|------|----|---|
| 001101 | 10010 | 10011 | 1000 0000 0000 0000|




The binary code was then converted to hex so that it could be used in the program.  

| 0011 | 0110 | 0101 | 0011 | 1000 | 0000 | 0000 | 0000|
|-----|-----|-----|-----|-----|-----|-----|-----|
| 3 | 6 | 5 | 3 | 8 | 0 | 0 | 0 |


Answer = 	0x36538000


This program was then run and tested, just like in Task 2 step 2 shown above.  

A screenshot of this test can be seen below: 


![alt tag](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/Task_3_Simulation.PNG "Task 3 Simulation")

This screenshot is the same as Task 2's screenshot up to 40ns.  After this point, the ori code can be seen at work.  The program is supposed to take the value stored at $S2, and "or" it will the immediate value x8000.  The immediate value x8000 can be seen in the instruction as the last 4 hex-bits.  It is also shown as the Y output in the extendChooser multiplexer.  Based on the Task 2 simulation, the value in $S2 must be 7.  Therefore, "or"ing 7 and x8000 should return a result of x8007, which clearly happens at 40ns.  

IT WORKS!!!

The waveform file for this simulation is shown [here](https://raw.githubusercontent.com/JohnTerragnoli/ECE281_CE5/master/task3_waveform_1.wcfg).  






#Documentation: 
C3C Sabin Park helped me figure out how to add the correct waveforms to the simulation.  

C3C Sabin Park and I brainstormed ideas on how to add the ori command.  We decided upon the idea to create another instantiation of the 2 input mux and to lengthen the ALUsrc signal.
