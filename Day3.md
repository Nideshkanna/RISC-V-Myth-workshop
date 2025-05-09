![image](https://github.com/user-attachments/assets/cc48a567-8279-4a15-ac05-9c249fe28d29)# Day 3: Digital Logic with TL-Verilog and Makerchip

## RV-D3SK1 – Combinational Logic in TL-Verilog using Makerchip

### RV_D3SK1_L0_Welcome
Welcome to Day 3! Today we’ll dive into how TL-Verilog on Makerchip streamlines combinational circuit design with high-level constructs and built-in visualization.

### RV_D3SK1_L1_Introduction to Logic Gates
1. **Logic Gates** are the fundamental building blocks of digital circuits. They accept one or more binary inputs and produce a binary output according to a logic function.  
   ![1](https://github.com/user-attachments/assets/e088b0d6-bcb4-4ce9-82f8-b5efb66c9736)  
   ![Screenshot from 2025-05-09 10-43-36](https://github.com/user-attachments/assets/d3e84391-1148-4c5d-9792-86cccbabb76e)

2. **Combinational Circuits** rely solely on current inputs, without memory elements, to determine outputs. Common gates include AND, OR, NOT, XOR, etc.  
   ![2](https://github.com/user-attachments/assets/13d39896-1824-49c1-8907-1723ade8c013) ![3](https://github.com/user-attachments/assets/0b0736eb-2036-4e39-8b9b-952340f89331)

*Example:* A **Full Adder** adds three bits (A, B, Cin) to produce Sum and Cout.

3. **Boolean Operators** connect logical expressions in both hardware and software design.  
   ![4](https://github.com/user-attachments/assets/ed26a2a4-edc1-4cf6-bfbb-1b18ca9d109b)

---

### RV_D3SK1_L2_Basic Mux Implementation and Introduction to Makerchip
- A **Multiplexer (MUX)** selects one of several inputs based on select signals:  
  ```verilog
  assign f = s ? X1 : X2;
  ```
- Makerchip offers an integrated TL-Verilog environment with instant compile, simulation, waveform view, and visual block diagrams.  
  ![Screenshot from 2025-05-09 11-03-31](https://github.com/user-attachments/assets/e7500bab-d116-4061-a1d0-e06a0cff0dcd)

---

### RV_D3SK1_L3_Labs for Combinational Logic

#### Inverter
Implement a simple inverter in TL-Verilog; observe how `!in` synthesizes to minimal logic.  
![123](https://github.com/user-attachments/assets/177eb9d6-f5fa-4c8d-9838-afd2059a5f35)

#### Boolean Gates
Test AND, OR, XOR with vector inputs:  
![456](https://github.com/user-attachments/assets/f4997923-c4c9-4767-b697-79386a2c1394)

#### Vectors
Create multi-bit buses (e.g., 5-bit vectors) and observe bit-wise operations.  
![vector](https://github.com/user-attachments/assets/218fc974-5ac5-4ac6-9bea-2649d2215651)

#### MUX Variants
1. **3-to-1 MUX** selecting one of three 3-bit inputs.  
   ![Screenshot from 2025-05-09 11-57-40](https://github.com/user-attachments/assets/9ced332d-9f1f-49b6-9370-de7cc472fa5b)  
2. **2-to-1 MUX** on 8-bit vectors.  
   ![Screenshot from 2025-05-09 12-00-47](https://github.com/user-attachments/assets/1d524faf-668a-415c-b396-4ea50fac9d3c)

#### Combinational Calculator
Build a simple calculator supporting `+`, `-`, `*`, `/` in pure combinational logic.  
![calc](https://github.com/user-attachments/assets/e88e0e93-fda3-4d5c-ba5e-2b9ddc76a83c)

---

## RV-D3SK2 – Sequential Logic

### RV_D3SK2_L1_Introduction to Sequential Logic and Counter Lab
Sequential elements (like flip-flops) capture state on clock edges.  
- **Fibonacci Series Lab**:  
  ```verilog
  $num[31:0] = $reset ? 1 : >>1$num + >>2$num;
  ```  
  ![Screenshot from 2025-05-09 12-08-18](https://github.com/user-attachments/assets/5cf47f5a-03c4-4169-a284-e33e43ddf6ea)

- **Free-Running Counter**: Increments a register each clock cycle.  
  ![Screenshot from 2025-05-09 12-13-51](https://github.com/user-attachments/assets/058c9b9a-90ca-4783-ab93-8a84a342d038)

---

### RV_D3SK2_L2_Sequential Calculator Lab
Extend the combinational calculator with registers to pipeline multi-stage operations.  
- Value literal formats (e.g., `16'hF0`).  
  ![calcs](https://github.com/user-attachments/assets/b63578ba-0bf1-4722-8af0-0bcbc7317f7f)  
  ![Screenshot from 2025-05-09 12-20-28](https://github.com/user-attachments/assets/33b21d97-7d31-434f-ad31-6b0d943c2724)

---

## RV-D3SK3 – Pipelined Logic

### RV_D3SK3_L1_Pipelined Logic and Re-Timing
Pipelining divides logic into stages, enabling higher clock frequencies. TL-Verilog makes this trivial with `|stage @1`, `@2`, etc.

### RV_D3SK3_L2_Pipeline Logic Advantages and Demo in Platform
- **Benefits**: Improved throughput, lower critical path, automated retiming.  
  ![pip](https://github.com/user-attachments/assets/1a2ecd34-c1c4-4345-abba-aa27083da1ba)

### RV_D3SK3_L3_Lab on Error Conditions within Computation Pipeline
Explore naming conventions and error checks:  
- `$pipe_signal` tokens, validity of identifiers, and timing-abstract error detection.  
  ![pip1](https://github.com/user-attachments/assets/ac7a1bb6-131e-4f3e-bfc5-a3f96452e064)

### RV_D3SK3_L4_Lab on 2-Cycle Calculator
Implement a two-stage pipeline for the calculator and verify timing correctness.  
![2calc](https://github.com/user-attachments/assets/4dcd4667-cccb-4081-8c72-e0113913582a)

---

## RV-D3SK4 – Validity

### RV_D3SK4_L1_Introduction to Validity and Its Advantages
The `?$valid` scope gates pipeline stages, improving error checking and enabling clock gating.

### RV_D3SK4_L2_Lab on Validity and Valid-When Condition
Add validity flags to the two-cycle calculator and observe transaction validity.  
![v1](https://github.com/user-attachments/assets/1e28e158-07c8-4d6b-be19-5150e04981b5)

### RV_D3SK4_L3_Lab to Compute Total Distance
Chain valid transactions through multiple stages to compute cumulative metrics.  
![v2](https://github.com/user-attachments/assets/07ff7eca-3751-4a66-8881-b7f232afbdcf)

### RV_D3SK4_L4_Lab on 2-Cycle Calculator with Validity
Combine pipeline and validity to build a robust staged calculator.  
![v3](https://github.com/user-attachments/assets/5609ea7c-3029-46b6-a3b3-a28db196d6f5)

### RV_D3SK4_L5_Calculator Single Value Memory Lab
Add a memory element to store and recall a single value within the pipeline.  
![v4](https://github.com/user-attachments/assets/38168f07-58b6-40aa-86f3-dd9f43bdba5b)

---

## RV Day 3 Wrap-up

### RV_D3SK5_L1_Introduction to Hierarchy Concept (Bonus)
Learn how to structure TL-Verilog modules hierarchically for large designs.

![Screenshot from 2025-05-09 12-55-47](https://github.com/user-attachments/assets/c8f06641-6664-4280-8713-8679ec3796fa)


### RV_D3SK5_L2_Day3_Closer
Recap key takeaways from Day 3 and preview for Day 4 - Basic RISC-V CPU micro-architecture.

