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

--------------
|00 1000|0 0000|1 0000|0000 0000 0000 1110|
------------
|00 1000|0 0001|1 0001|0000 0000 1101 1011|
---------------
|00 0000|1 0000|1 0001|1 0010|0 0000|10 0000|
---------------
|10 1011|0 0000|1 0010|0000 0000 0101 0100|
```


