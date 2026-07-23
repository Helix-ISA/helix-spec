# Instruction set

---

## Design Considerations

To enforce deterministic behavior and prevent undefined behavior the full zero instruction
(**00000000000000000000000000000000**) will be reserved as an illegal instruction. Consequently,
any execution jump into an uninitialized or zeroed memory region will explicitly trigger an illegal
instruction trap.
