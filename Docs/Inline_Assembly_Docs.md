# ARM Cortex-M4 Assembly Programming Guide

## Table of Contents
1. [Key Features](#key-features)
2. [Register Set](#register-set)
3. [Inline Assembly Syntax](#inline-assembly-syntax)
4. [Common Instructions](#common-instructions)
5. [Memory Access](#memory-access)
6. [Control Registers](#control-registers)
7. [Examples](#examples)
8. [Best Practices](#best-practices)

---

## Key Features
- **Thumb-2 Instruction Set**: Mixed 16-bit and 32-bit instructions for code density and performance  
- **Harvard Architecture**: Separate instruction and data buses  
- **Single-Cycle Multiply**: Hardware multiplier (32x32 → 64-bit)  
- **Floating-Point Unit (FPU)**: Optional in Cortex-M4 (single-precision)  
- **NVIC**: Nested Vectored Interrupt Controller for low-latency interrupts  

---

## Register Set

| Register    | Alias | Purpose                             |
|-------------|-------|-------------------------------------|
| R0-R12      | -     | General-purpose registers           |
| R13         | SP    | Stack Pointer (MSP/PSP)             |
| R14         | LR    | Link Register (stores return addr)  |
| R15         | PC    | Program Counter                     |
| xPSR        | -     | Program status register             |
| PRIMASK     | -     | Interrupt mask register             |
| FAULTMASK   | -     | Fault mask register                 |
| BASEPRI     | -     | Base priority mask register         |
| CONTROL     | -     | Privilege and stack control         |

### Inline Assembly Syntax

**Basic Structure - 

'''asm

__asm volatile (
    "instruction1 \n"
    "instruction2 \n"
    : [outputs]  // "=r" (c_var)
    : [inputs]   // "r" (c_var)
    : [clobbers] // "r0", "memory"
);

### Special Register Access:
```asm
MRS R0, CONTROL     ; Read CONTROL into R0  
MSR CONTROL, R1     ; Write R1 into CONTROL  

'''
