Lab4_PRISM
==========
# ALU Simulation
## Discussion of ALU Modifications
The PRISM ALU (Arithmatic Logic Unit) was built to perform 8 operations including: AND, NEG (2s complement), NOT (invert), ROR, OR, IN, ADD, LD. Below is the output for a working ALU simulation. 

The arithmatic operation performed on the operand by the ALU is controlled by the OPCODE, labeled OpSel below. The following list matches the opcode with the desired operation.


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

In order to implement each of these operations, VHDL code was written. Fortunately, VHDL contains built in commands that perform all the above operations except NEG. NEG was implemented based on the fact that 2s compliment conversions are based on the operation of flipping all the bits and adding 1. Below is the code that assigns the output to the accumulator based on the given OPcode (OpSel).

```
Result <= (Data and Accumulator) when OpSel = "000" else
			 Not Accumulator + 1 when OpSel = "001" else
			 Not Accumulator when OpSel = "010" else
			 std_logic_vector(rotate_right(unsigned(Accumulator), 1)) when OpSel = "011" else
			 Data or Accumulator when OpSel = "100" else
			 Data when OpSel = "101" else
			 Data + Accumulator when OpSel = "110" else
			 Data when OpSel = "111";
```

## ALU Test and Debug
In order to test the functionality of the ALU it was run through a testbench provided be Capt Silva. The testbench cycled through all seven possible OpSels for various operands. The correctness of the ALU was then determined with a manual check. I.E. when the opcode is "100" is the Data "Ored" together?

![alt tag](https://raw.githubusercontent.com/seanbapty/Lab4_PRISM/master/ALU%20out.JPG)
