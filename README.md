ECE281_CE5
==========


#**Task 1**
The purpose of this task was to initialize the registers $S0 and $S1 with the decimal values 44 and -37 respectively.  To add and store the result in $S2.  Then, this value at $S2 will be stored at the hexadecimal memory address x54.  The MIPS code below performs the desired actions: 

```
addi $S0, $0, 44
addi $S1, $0, -37
addi $S2, $0, $1
sw $S2, 0X54($0)
```
