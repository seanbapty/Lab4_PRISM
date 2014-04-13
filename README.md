Reverse Engineering
==========
# ALU Simulation
## ALU Modifications
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

Fortunatly, except for minor syntaxual errors, there was no debugging needed to remedy the operation of the ALU.

## Datapath Modifications 
The next task in the lab was to implement the datapath of the PRISM architecture. PRISM is composed of 5 main registers, the Instruction Register, the Memory Address Register High, the Memory Address Register Low, the Program Counter, and the Resiger Accumulator attached to the ALU. The instruction register stores the opcode of the current instruction based on input from the IR load signal, and then passes the output to the instruction register. The memory address register recieves data from the data bus and then sends that data to the jump selector multiplexer. The jump selector multiplexer chooses between the concated output from the memory address register high and the memory address register low and then passes the 8 bit result to the program counter. The program counter keeps track of what step the program is on. It passes the output when PC load is high. The signal then passes to the address select multiplexer. Here a control signal chooses betweeen the concated memory address registers, and the program counter. The output of this multiplexer is then passed to the address bus. In each of these stages given code included all the necessary steps except the assinment of sginals to the respective register. 
The register accumulator is the memory part of the ALU and stores the output of the opcode determined arithmatic operation.
Below is a schematic of the entire prism architecture.

![alt tag](https://raw.githubusercontent.com/seanbapty/Lab4_PRISM/master/PRISM%20schematic.JPG)

## Datapath Testbench
In this lab the testbench code was provided, as was the necessary internal signals.
The functionality of the first 50ns of the simularion was cross refernenced with an exemplar picture.

![alt tag](https://raw.githubusercontent.com/seanbapty/Lab4_PRISM/master/part2.JPG)
