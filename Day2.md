# Day 2: Introduction to ABI and Basic Verification Flow

## RV-D2SK1 - Application Binary Interface (ABI)

### RV-D2SK1_L1: Introduction to ABI
The **Application Binary Interface (ABI)** defines the low-level interface between application code and the underlying hardware or operating system. It specifies:
- Calling conventions (how functions receive parameters and return values).
- Register usage and conventions.
- Memory layout and data type sizes.

In a typical software-to-hardware flow:
```
Applications → Standard Libraries → OS → ISA (RISC-V/ARM/x86) → Hardware (RTL)
```
Each arrow represents an interface layer (APIs, ABIs/System Call Interface, ISAs, RTL).

RISC-V provides **32 integer registers** accessed via ABI names.  
- **XLEN** determines register width: 32-bit for RV32, 64-bit for RV64.

### RV-D2SK1_L2: Memory Allocation for Double Words
On RV64 (XLEN=64), double words (64-bit values) can be:
1. Stored directly in a 64-bit register.
2. Stored in memory across eight consecutive bytes (`m[0]` holds LSB, `m[7]` holds MSB in little-endian order).

For an array of three double words:
```
Bytes 0–7   → First double word
Bytes 8–15  → Second double word
Bytes 16–23 → Third double word
```
To load the third double word (bytes 16–23) into register `x8` using base register `x23`:
```assembly
ld x8, 16(x23)
```

### RV-D2SK1_L3: Load, Add, and Store Instructions
#### Load Double Word (I-type)
```assembly
ld x8, 16(x23)
```
| immediate [31:20] | rs1 (x23) [19:15] | funct3 [14:12] | rd (x8) [11:7] | opcode (ld) [6:0] |

#### Register-Register Add (R-type)
```assembly
add x8, x24, x8
```
| funct7 [31:25] | rs2 (x8) [24:20] | rs1 (x24) [19:15] | funct3 [14:12] | rd (x8) [11:7] | opcode (add) [6:0] |

#### Store Double Word (S-type)
```assembly
sd x8, 8(x23)
```
| imm[11:5] [31:25] | rs2 (x8) [24:20] | rs1 (x23) [19:15] | funct3 [14:12] | imm[4:0] [11:7] | opcode (sd) [6:0] |

**Instruction Formats:**
- **R-type**: Register-register (e.g., `add`).
- **I-type**: Register and immediate (e.g., `ld`).
- **S-type**: Store with register and immediate (e.g., `sd`).

With 5 bits for each register field (`rs1`, `rs2`, `rd`), RISC-V supports **2^5 = 32 registers**.

---

## RV-D2SK2 - Lab Work: Custom Sum Algorithm in Assembly

### RV-D2SK2_L1: C Program with Assembly Function
The main C program passes parameters in registers `a0` and `a1` to an external assembly function `load`, which computes the sum from 1 to *n* and returns the result in `a0`.

**1to9_custom.c**
```c
#include <stdio.h>
extern int load(int x, int y);

int main() {
    int count = 9;
    int result = load(0x0, count + 1);
    printf("Sum from 1 to %d is %d\n", count, result);
    return 0;
}
```

**load.S**
```assembly
    .section .text
    .global load
    .type load, @function
load:
    add a4, a0, zero      # a4 = a0
    add a2, a0, a1        # a2 = a0 + a1
    add a3, a0, zero      # a3 = a0 (loop counter)
loop:
    add a4, a3, a4        # accumulate: a4 += a3
    addi a3, a3, 1        # a3++
    blt a3, a2, loop      # if a3 < a2, repeat
    add a0, a4, zero      # move result to a0
    ret                   # return
```

### RV-D2SK2_L2: Compilation and Simulation
```bash
# Compile C and assembly together
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o 1to9_custom.o 1to9_custom.c load.S

# Run on Spike simulator
spike pk 1to9_custom.o

# Disassemble and inspect
riscv64-unknown-elf-objdump -d 1to9_custom.o | less
```

---

## RV-D2SK3 - Basic Verification Flow using Icarus Verilog (iverilog)

In this lab, we run our C-generated program on a RISC-V CPU core written in Verilog (e.g., PicoRV32) and verify its execution.

### Setup and Execution
1. **Clone Verification Collaterals**  
   ```bash
   git clone https://github.com/kunalg123/riscv_workshop_collaterals.git
   cd riscv_workshop_collaterals/labs
   ```

2. **Inspect and Prepare Files**  
   ```bash
   ls -ltr
   vim picorv32.v       # RISC-V CPU core implementation
   vim testbench.v      # Testbench for simulation
   vim rv32im.sh        # Shell script to assemble and run tests
   ```

3. **Run Verification Script**  
   ```bash
   chmod +x rv32im.sh
   ./rv32im.sh
   ```
   This script compiles the CPU core and testbench with `iverilog`, runs the simulation, and displays outputs for analysis.

---

*End of Day 2 Summary*
