# Instruction Encoding

## Overview

The Helix instruction encoding defines the binary representation of every instruction executed by
the processor.

Helix ISA v1.0 uses **fixed-width 32-bit instructions**. Every instruction occupies exactly one
32-bit word in memory regardless of its operation.

---

## Bit Ordering

Instruction bits are numbered from the most significant to least significant.

```text
31                       7 6     0
+--------------------------------+
|       Instruction       |OpCode|
+--------------------------------+
```

The instructions are ordered in this way so in a later ISA version we can add compression.

---

## Instruction Blocks

* opcode: The instruction type
* rs1-2: Source registers
* rd: Destination register
* imm: Immediate values / constants
* funct3: Type operations
* funct7: More operation granularity

---

## Instruction Types

The instructions encodings may look a little weird splitting up funct entries and imm entries.
This is so decoding is faster an easier for register instructions since they are always occupy the
same bytes. Example: rd is always 7:11 when a destination register is required.

### R-Type
Register to register instructions (arithmetic/logic) (addr, subl, srl, sll...).

```text
31   25 24 20 19 15 14   12 11 7 6     0
+--------------------------------------+
|funct7| rs2 | rs1 |funct3 | rd |OpCode|
+--------------------------------------+
```

### I-Type
Immediate to register and loading instructions (more operations, less precision)
(lb, lh, lw, ld, addi, andi).

```text
31         20 19 15 14   12 11 7 6     0
+--------------------------------------+
|  imm[11:0] | rs1 |funct3 | rd |OpCode|
+--------------------------------------+
```

### S-Type
Storing data in system memory (stoi, stor, ).

```text
31      25 24 20 19 15 14   12 11     7 6     0
+---------------------------------------------+
|imm[11:5]| rs2 | rs1 |funct3 |imm[4:0]|OpCode|
+---------------------------------------------+
```

### U-Type
Loading larger immediates into a register with targets (lui, lli, lmi...).

```text
31                  12 11      7 6       0
+---------------------+---------+--------+
|      imm[31:12]     |   rd    | opcode |
+---------------------+---------+--------+
```

### B-Type
Branching instructions (bne, be, bge...)

```text
 31      25 24   20 19   15 14  12 11      7 6      0
+----------+-------+-------+------+---------+--------+
|imm[12,10:5]|rs2   |  rs1  |funct3|imm[4:1,11]|opcode|
+----------+-------+-------+------+---------+--------+
```

Immediate bit 12 is the signed bit indicating positive or negative offset
Immediate bit 11 is stored differntly since 12 is the last bit in the instruction.
Immediate bit 0 isn't needed since the value will always be 0 since instructions are on the half
word alignment (2 bytes) to allow compressed 16 bit instructions later.

### J-Type
Jump instructions (ljmp, jmp...).

```text
31                  12 11 7 6       0
+---------------------+----+--------+
imm[20,10:1,11,19:12] | rd | opcode |
+---------------------+----+--------+
```
