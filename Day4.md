# Day 4: Basic RISC-V CPU Micro-architecture

## RV-D4SK1 – Introduction to Simple RISC-V Micro-architecture

### RV_D4SK1_L1_Micro-architecture of Single-Cycle RISC-V CPU
Today we examine the high-level block diagram of a single-cycle RISC-V CPU. We discuss how each instruction completes in one clock cycle—fetch, decode, execute, memory access, and write-back stages all occur in parallel hardware structures.
![image](https://github.com/user-attachments/assets/b0384a00-36ed-46f3-9620-5f201778688b)
The example RISC-V Block Diagram

### RV_D4SK1_L2_Starting Point Code for RISC-V Labs Part-1  
You’ll begin with a Verilog skeleton that includes:  
- A program counter (PC) register.  
- An instruction memory block pre-loaded with a simple test program.  
- A register file module stub.  
- A basic ALU interface.  
This scaffold lets you focus on fleshing out fetch and decode logic first.

   ![Screenshot from 2025-05-09 19-21-46](https://github.com/user-attachments/assets/89e1374e-b63a-4095-8aa5-939adeb64a81)



### RV_D4SK1_L3_Starting Point Code for RISC-V Labs Part-2  
The second starter file adds:  
- Control signals for ALU operations.  
- A data memory interface.  
- Pipeline register placeholders for future pipelined extensions.  
Use this as the basis for implementing register-file read/write and ALU behavior.
   ![41](https://github.com/user-attachments/assets/9bd74bce-7256-4c22-95f5-86754597b017)
---
   ![42](https://github.com/user-attachments/assets/44487020-979f-4523-80ac-30222aac77e2)
---
   ![43](https://github.com/user-attachments/assets/1bedb11b-e70c-4bc7-aa9f-40d84ba63ba6)


## RV-D4SK2 – Fetch and Decode

### RV_D4SK2_L1_Implementation Plan and Lab for PC  
We detail how the PC increments by 4 each cycle and jumps on branches. In lab, you’ll:  
1. Initialize PC to 0 on reset.  
2. Create logic to update PC ← PC + 4 or PC ← target on branch.

   ![44](https://github.com/user-attachments/assets/b959ad28-1479-4b71-ac8f-b38aca0b59f5)


### RV_D4SK2_L2_Lab for Instruction Fetch Logic  
Wire the instruction memory output to your fetch stage. Verify that for each clock, the CPU reads the correct 32-bit instruction from address PC.

   ![45](https://github.com/user-attachments/assets/13548797-d011-40b5-b70d-1bef45898eb7)


### RV_D4SK2_L3_Lab for RV Instruction-Type (R, I, S, B, U, J) Decode Logic  
Implement the top-level decode:  
- Extract opcode[6:0] and funct3[14:12].  
- Classify instructions into R, I, S, B, U, or J types.  
- Route fields to the appropriate immediate-generator or register-address modules.

  ![46](https://github.com/user-attachments/assets/c0d41c66-8772-4714-9253-ed502c836e6f)


### RV_D4SK2_L4_Lab for Instruction Immediate Decode Logic for RV-ISBUJ  
Build the immediate-generator unit:  
- Sign-extend I-type immediates.  
- Assemble S/B/U/J immediates by concatenating instruction bits.  
- Test each format against known encodings.

   ![49](https://github.com/user-attachments/assets/2103904b-8855-4615-a727-d5f5319ac213)



### RV_D4SK2_L5_Lab to Decode Other Fields of Instructions for RV-ISBUJ  
Within each instruction class, decode:  
- Source registers rs1/rs2 from bits [19:15]/[24:20].  
- Destination register rd from bits [11:7].  
- funct7[31:25] for R-type ALU sub-operations.

  ![47](https://github.com/user-attachments/assets/840cc2a3-0339-49ee-a703-296aa94f054e) 


### RV_D4SK2_L6_Lab to Decode Instruction Field Based on Instr Type RV-ISBUJ  
Combine your immediate-generator and register-field decoders into a unified decode module that outputs a full control word and operand indices for the datapath.

![48](https://github.com/user-attachments/assets/52f76d72-1ecd-4504-8a08-c089cde31f4a)

### RV_D4SK2_L7_Lab to Decode Individual Instruction  
Finally, map each control word to concrete actions:  
- ALU operation select.  
- MemRead/MemWrite enable.  
- Branch condition signals.

![50](https://github.com/user-attachments/assets/6c3b03f0-3de2-4bb2-9d7a-15ac1d48861f)


---

## RV-D4SK3 – RISC-V Control Logic

### RV_D4SK3_L1_Lab for Register File Read Part-1 (USE UPDATED SHELL CODE)  
Implement the first half of the register-file read port:  
- Two read addresses (rs1, rs2) → two read data outputs.  
- Connect these outputs to the ALU inputs.

### RV_D4SK3_L2_Lab for Register File Read Part-2  
Add support for read-after-write hazards: ensure that in the same cycle writes to rd reflect immediately on reads.

 ![51](https://github.com/user-attachments/assets/0c30eb5e-f4ba-4408-b39a-178c8be527d3)


### RV_D4SK3_L3_Lab for ALU Operations for ADD/ADDI  
Implement ALU operations:  
- R-type ADD: operand1 + operand2.  
- I-type ADDI: operand1 + immediate.  
Test edge cases like overflow and negative results.

 ![52](https://github.com/user-attachments/assets/b8665257-22fe-44cb-84f5-283166f74aec)


### RV_D4SK3_L4_Lab for Register File Write  
Wire the ALU result and memory data back into the register file’s write port (rd) when RegWrite is asserted.

### RV_D4SK3_L5_Concept of Array and Register File Details  
Discuss the register file as an array of 32 64-bit registers in RV64, each indexed by a 5-bit address; examine how x0 is hardwired to zero.

### RV_D4SK3_L6_Lab for Implementing Branch Instructions  
Implement branch comparators (BEQ, BNE, BLT, BGE) by comparing read data and generating a branch-taken signal to redirect PC.

### RV_D4SK3_L7_Lab for Completing Branch Instruction Implementation  
Connect the branch-taken signal to PC update logic; test with simple loop programs to verify correct branching.

![53](https://github.com/user-attachments/assets/2ec0cb3c-78b5-4a3d-88e4-05e04e0a34f4)

The above labs 4,5,6,7 were impletemented in the design.

### RV_D4SK3_L8_Lab to Create Simple Testbench  
Write a Verilog testbench that:  
1. Instantiates your CPU top module.  
2. Drives a clock and reset.  
3. Loads a small instruction memory.  
4. Asserts pass/fail based on register file contents after program execution.

![54](https://github.com/user-attachments/assets/a98236c4-ab7e-45d9-842e-b132270dd6ab)


---

*End of Day 4 Summary*  
