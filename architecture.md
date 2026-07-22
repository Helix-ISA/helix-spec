# Helix Architecture

## Overview

Helix is a 64-bit RISC instruction set architecture. The base architecture uses fixed-width 32-bit
instructions, providing straightforward instruction decoding, predictable execution, and efficient
hwardware implementation. A future extension will introduce optional 16-bit compact instructions to
improve code density while remaining fully compatible with the 32-bit base ISA.

Rather than carrying decades of legacy design decisions, Helix is built with a clean architectural
foundation intended for both education and practical system development. The architecture
prioritizes a regular instruction encoding, an orthogonal design, and behavior that is easy to
understand, implement, and optimize.

Helix is not intended to be only a processor architecture. It is a complete computing platform
developed from the ground up, including the software toolchain, hardware implementations, firmware,
operating system support, and development tools. By controlling the entire ecosystem, the project
aims to provide a coherent platform for experimentation, research, and real-world applications
while maintaining a stable and well-defined specification.

---

## Architectural Goals

Helix is designed to:

* Eliminate unnecessary historical complexity.
* Maintain predictable and consistent behavior.
* Be straightforward to implement in both software and hardware.
* Support the development of complete computer systems, from firmware to operating systems.
* Encourage experimentation with architectural features while preserving compatibility within a major ISA version.

---

## Architectural Scope

The Helix project is more than the instruction set and hardware that it runs on. The long-term
ecosystem includes:

* ISA specification
* Assembler
* Linker
* Emulator
* Compiler toolchain
* Hardware implementation
* FPGA implementation
* Operating system
* Development tools
* Documentation and educational materials

Each component is intended to be developed from the specification upward, ensuring that the system
reflects the same architectural principles.

