Lab4_PRISM
==========
# ALU Simulation
The PRISM ALU was built to perform 8 operations including: AND, NEG (2s complement), NOT (invert), ROR, OR, IN, ADD, LD. Below is the output for a working ALU simulation. 
![alt tag](https://raw.githubusercontent.com/seanbapty/Lab4_PRISM/master/ALU%20out.JPG)

The arithmatic operation performed by the ALU is controlled by the OPCODE, labeled OpSel below. The following list matches the opcode with the desired operation.


| OPcode | Instruction        | 
|--------|--------------------|
| 0      | AND                | 
| 1      | NEG (2s complement)| 
| 2      | NOT (invert)       |  
| 3      | ROR                | 
| 4      | OR                 | 
| 5      | IN                 | 
| 6      | ADD                | 
| 7      | LD                 | 

In order to implement each of these operations, VHDL code was written. Fortunately, VHDL contains built in commands that perform all the above operations except NEG. NEG was implemented based on the fact that 2s compliment conversions are based on the operation of flipping all the bits and adding 1.
