# Digital Logic with TL-Verilog and Makerchip
## 1) Combinational logic in TL-Verilog using Makerchip
### L1. Introduction to Logic Gates
1.**Logic Gates** are *fundamental building blocks* for digital circuits which take one or more inputs (1s or 0s) and give an output based on the logic.

   ![1](https://github.com/user-attachments/assets/e088b0d6-bcb4-4ce9-82f8-b5efb66c9736)

   ![Screenshot from 2025-05-09 10-43-36](https://github.com/user-attachments/assets/d3e84391-1148-4c5d-9792-86cccbabb76e)



2.**Combinational circuits** are complex digital circuits that rely on fundamental building blocks, such as logic gates (AND, OR, NOT, XOR, etc.). They determine their outputs solely based on current inputs, without utilizing any memory or feedback mechanisms.

  ![2](https://github.com/user-attachments/assets/13d39896-1824-49c1-8907-1723ade8c013)  ![3](https://github.com/user-attachments/assets/0b0736eb-2036-4e39-8b9b-952340f89331)


*Example*: Full Adder (adds 3 bits together) :
- Inputs: A, B, Cin (carry-in)  
- Outputs: S (sum), Cout (carry-out)

3.**Boolean Operators** are logical connectors used to evaluate conditions in programming and digital logic.

  ![4](https://github.com/user-attachments/assets/ed26a2a4-edc1-4cf6-bfbb-1b18ca9d109b)


------

### L2. Basic Mux Implementation And Introduction To Makerchip
- A **MUX (Multiplexer)** selects one from multiple inputs and forwards it to a single output based on control or select signals. It's like a data switch!
- Its Verilog syntax is : assign f = s ? X1 : X2;

**Navigation through Makerchip** 

![Screenshot from 2025-05-09 11-03-31](https://github.com/user-attachments/assets/e7500bab-d116-4061-a1d0-e06a0cff0dcd)


### L3.1  Labs for Cominational Logic
**Example: Pythagores Theorem** 
![Screenshot from 2025-05-09 11-05-30](https://github.com/user-attachments/assets/dd5571c4-d433-4175-b8a0-58c55dc34bae)


#### Inverter
![123](https://github.com/user-attachments/assets/177eb9d6-f5fa-4c8d-9838-afd2059a5f35)



#### Other logic : Boolean operators ( && , || , ^ )
![456](https://github.com/user-attachments/assets/f4997923-c4c9-4767-b697-79386a2c1394)
   


### L3.2  Vectors
**Vectors of 5 bits**
![vector](https://github.com/user-attachments/assets/218fc974-5ac5-4ac6-9bea-2649d2215651)


### L3.3  Mux
**1.[ 2:0 ] Mux**
  ![Screenshot from 2025-05-09 11-57-40](https://github.com/user-attachments/assets/9ced332d-9f1f-49b6-9370-de7cc472fa5b)

 
**2. [ 7:0 ] Mux**
   ![Screenshot from 2025-05-09 12-00-47](https://github.com/user-attachments/assets/1d524faf-668a-415c-b396-4ea50fac9d3c)

   
### L3.4  Combinational Calculator
  ![calc](https://github.com/user-attachments/assets/e88e0e93-fda3-4d5c-ba5e-2b9ddc76a83c)


-----

## 2) Sequential Logic 
### L1.  Introduction to Sequential Logic and Counter Lab 
Sequential logic is sequenced by a clock signal.
Example: D-flip-flop transition next state to current state on a rising clock edge
The circuit is constructed to enter a known state in response to a reset signal.

#### Fibonacci Series LAB
-Next value is sum of previous two: 1,1,2,3,5,8,13... { $num[31:0] = $reset ? 1 : >>1$num + >>2$num; }
  ![Screenshot from 2025-05-09 12-08-18](https://github.com/user-attachments/assets/5cf47f5a-03c4-4169-a284-e33e43ddf6ea)

#### Counter LAB
  ![Screenshot from 2025-05-09 12-13-51](https://github.com/user-attachments/assets/058c9b9a-90ca-4783-ab93-8a84a342d038)


### L2.  Sequential Calculator Lab
Values in Verilog
eg: 16'hFO where 16 - 16-bits; h - hexadecimal; FO - value 
   ![calcs](https://github.com/user-attachments/assets/b63578ba-0bf1-4722-8af0-0bcbc7317f7f)

   ![Screenshot from 2025-05-09 12-20-28](https://github.com/user-attachments/assets/33b21d97-7d31-434f-ad31-6b0d943c2724)


-----

## 3)  Pipelined logic
### L1. Pipelined Logic And Re-Timing
- **Pipeline logic** refers to the structured approach of breaking down a process into sequential stages, where each stage processes data and passes it to the       next. This technique is widely used to improve efficiency and throughput.
- In the comparison between **SystemVerilog and TL-Verilog**, the code reduction property of TL-Verilog offers a significant advantage over SystemVerilog. This reduction minimizes bugs and accelerates the design process, making development more efficient.

### L2. Pipeline Logic Advantages And Demo In Platform
- Pipeline logic enhances efficiency by breaking tasks into stages, enabling parallel execution.
- It speeds up processing, optimizes resource use, reduces latency, improves scalability, and supports automation in workflows.
   ![pip](https://github.com/user-attachments/assets/1a2ecd34-c1c4-4345-abba-aa27083da1ba)

### L3. Lab On Error Conditions Within Computation Pipeline
- **Identifier Type Determination** – The type of an identifier is defined by its symbol prefix and case/delimitation style.
- **Example Breakdown** – `$pipe_signal`  
   - **Symbol Prefix:** `$`  
   - **Delimitation Style:** `_`  
   - **Tokens:** `pipe`, `signal`
- **Delimitation Styles Based on First Token:**  
   - `$lower_case` → pipe signal  
   - `$CamelCase` → state signal  
   - `$UPPER_CASE` → keyword signal  
- **Numbers Affect Tokens:**  
   - `$base64_value` is valid  
   - `$bad_name_5` is invalid
- **Numeric Identifiers:**  
   - `>>1` represents "ahead by 1".
    ![pip1](https://github.com/user-attachments/assets/ac7a1bb6-131e-4f3e-bfc5-a3f96452e064)

### L4. Lab On 2-Cycle Calculator

![2calc](https://github.com/user-attachments/assets/4dcd4667-cccb-4081-8c72-e0113913582a)


----

## 4)  Validity
### L1. Introduction To Validity And Its Advantages
### L2. Lab On Validity And Valid When Condition

   ![v1](https://github.com/user-attachments/assets/1e28e158-07c8-4d6b-be19-5150e04981b5)


### L3. Lab To Compute Total Distance

   ![v2](https://github.com/user-attachments/assets/07ff7eca-3751-4a66-8881-b7f232afbdcf)


### L4. Lab on 2-cycle Calculator with Validity

  ![v3](https://github.com/user-attachments/assets/5609ea7c-3029-46b6-a3b3-a28db196d6f5)

### L5. Calulator Single Value Memory Lab

  ![v4](https://github.com/user-attachments/assets/38168f07-58b6-40aa-86f3-dd9f43bdba5b)













