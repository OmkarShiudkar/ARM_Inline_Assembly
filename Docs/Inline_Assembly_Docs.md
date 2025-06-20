# ARM Cortex-M4 Assembly Programming Guide

## Table of Contents
1. [Key Features](#key-features)
2. [Register Set](#register-set)
3. [Inline Assembly Syntax](#inline-assembly-syntax)
4. [Common Instructions](#common-instructions)
5. [Control Registers](#control-registers)
6. [Examples](#examples)
7. [Best Practices](#best-practices)

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

## Inline assembly syntax

**Basic Structure** - 

```asm

__asm volatile (
    "instruction1 \n"
    "instruction2 \n"
    : [output operands]  /* Optional */
    : [input operands]   /* Optional */
    : [clobber list]     /* Optional */
);

```

| Constraint  | Purpose                             |
|-------------|-------------------------------------|
| "=r"        |     Write-only register             |
| "+r"        |     Read-write register             |
| "r"         | 	Input register                  |
| "m"         |     Memory operand                  |


### Special Register Access:
```asm
MRS R0, CONTROL     ; Read CONTROL into R0  
MSR CONTROL, R1     ; Write R1 into CONTROL  

```
### common-instructions:

| Instruction    | Example | Description                             |
|-------------|-------|-------------------------------------|
| MOV     | MOV R0, #42   | Move immediate value           |
| ADD         | ADD R0, R1, R2    | Addition           |
| SUB         | SUB R0, R1, R2    | Subtraction |
| MUL         | MUL R0, R1, R2    | Multiply   |
| LDR        | LDR R0, [R1]     | Load from memory |
| STR     | STR R0, [R1]    | Store to memory|
| BL   | BL function    | Branch with link    |
| BX     | BX LR    |Return from function   |
| CMP     |CMP R0, R1     | Compare    |
|PUSH       |PUSH {R0-R4} | Push to stack|
|POP        |POP {R0-R4}|Pop from stack|