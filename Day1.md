# Day 1: Introduction to RISC-V ISA and GNU Compiler Toolchain

## RV-D1SK1 - Introduction to RISC-V Basic Keywords

### RV_D1SK1_L1_Introduction
1. Overview of the RISC-V Instruction Set Architecture (ISA).
2. RISC-V Architecture (C) → Implementation (RTL, e.g., PicoRV32 core) → Layout (qflow for hardware).
3. Layer mapping: Application layer → System software → Hardware layer.

### RV_D1SK1_L2_From Apps To Hardware
1. Software stack:  
   - Applications → System Software → OS → High-level languages (C, C++, Java, VB) → Compiler → ISA → Assembler  
2. Hardware flow:  
   - RTL snippet (understands instructions like `add x6, x10, ...`) → Synthesized netlist → Physical design implementation.  
3. Course outline:  
   - Part 1: RISC-V ISA  
   - Part 2: RTL & Synthesis of RISC-V CPU core (PicoRV32)  
   - Part 3: Physical design implementation of PicoRV32  

### RV_D1SK1_L3_Detailed Description of Course Content
1. C program examples and compilation.  
2. Instruction categories:  
   - Base Integer Instructions (RV64I)  
   - Pseudo instructions  
   - Multiply extension (RV64M)  
   - Floating-point extensions (RV64F & RV64D)  
3. Application Binary Interface (ABI) registers (`a0`, `ra`, etc.).  
4. Memory allocation & stack pointer usage (`a1`, `sp`, offsets).

---

## RV-D1SK2 - Labwork for RISC-V Software Toolchain

### RV_D1SK2_L1: C Program to Compute Sum from 1 to N
![Screenshot from 2025-05-03 20-17-25](https://github.com/user-attachments/assets/8c2ada96-aa8f-4a13-99c3-d2f019390829)


```c
#include <stdio.h>

int main() {
    int i, sum = 0, n = 5;
    for (i = 0; i <= n; i++) {
        sum += i;
    }
    printf("Sum of 1 to %d is %d", n, sum);
    return 0;
}
```

Compile and run natively:
```bash
gcc sum1ton.c
./a.out
```
![Screenshot from 2025-05-03 20-18-19](https://github.com/user-attachments/assets/bf07b9f4-a880-4b08-a430-baa786e0c84b)


### RV_D1SK2_L2: RISC-V GCC Compile and Disassemble
![Screenshot from 2025-05-03 20-59-34](https://github.com/user-attachments/assets/d9cbb72b-1da5-4ee0-9801-0b876537880a)


Compile for RISC-V:
```bash
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
riscv64-unknown-elf-objdump -d sum1ton.o | less
```
![Screenshot from 2025-05-03 20-59-48](https://github.com/user-attachments/assets/94455357-8888-4858-82f1-85b414028fa4)
![Screenshot from 2025-05-03 20-59-58](https://github.com/user-attachments/assets/8938435d-fdc3-4e78-9eb8-593549647092)


- Searching in `main()` reveals ~15 instructions.

![Screenshot from 2025-05-03 21-00-15](https://github.com/user-attachments/assets/ad4b39b8-a5fc-4622-83cf-3364c6284a14)



- With `-Ofast` optimization:
![Screenshot from 2025-05-03 21-00-43](https://github.com/user-attachments/assets/d77d38a5-3fb1-4247-87a7-d7b5bda559f4)


```bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```
- Now only ~12 instructions in `main()`.
![Screenshot from 2025-05-03 21-01-08](https://github.com/user-attachments/assets/37b880ee-011b-4508-ac5a-6b53d67f78fa)


### RV_D1SK2_L3: Spike Simulation and Debug
- Run on Spike:
  ```bash
  spike pk sum1ton.o
  ```
![Screenshot from 2025-05-03 21-02-44](https://github.com/user-attachments/assets/f5945693-c427-4a25-a514-4a86efc5bae2)


- Start Spike debugger:
  ```bash
  spike -d pk sum1ton.o
  ```
- Example debugger commands:
  ```
  :until pc 0x0100b0   # Stop before main()
  :reg a2             # View register a2
  ```
- Common instructions:
  - `lui a0, %hi(.LC1)`
  - `addi a0, a0, %lo(.LC1)`
 
![Screenshot from 2025-05-03 21-07-27](https://github.com/user-attachments/assets/9c7f11de-8ca4-41ad-807d-30f0579d828e)


---

## RV-D1SK3 - Integer Number Representation

### RV_D1SK3_L1: 64-bit Unsigned Numbers
- **Double Word (64-bit):** Range 0 to 2^64 - 1.

### RV_D1SK3_L2: 64-bit Signed Numbers
- MSB = 0 → positive; MSB = 1 → negative.
- Two's complement procedure:
  1. Binary representation.
  2. Invert bits (1's complement).
  3. Add 1.

### RV_D1SK3_L3: Lab for Signed and Unsigned Numbers

| Data Type                | Memory (Bytes) | Format Specifier |
|--------------------------|----------------|------------------|
| `unsigned int`           | 4              | `%u`             |
| `int`                    | 4              | `%d`             |
| `unsigned long long int` | 8              | `%llu`           |
| `long long int`          | 8              | `%lld`           |
