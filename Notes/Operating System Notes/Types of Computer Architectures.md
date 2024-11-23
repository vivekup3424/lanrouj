---
id: Types of Computer Architectures
aliases: []
tags:
  - cpu
  - architecture
---

# CPU Architectures Overview

### CISC (Complex Instruction Set Computing)
- Used by x86, x86_64 (AMD64)
	- **How it started**
		- X86 started out as a 16-bit instruction set for 16-bit processors, but has grown to 32-bit instruction sets. The term "x86" comes from the 8086, an early processor released by Intel. 
		- The names of several successors to the 8086 processor end in "86", including the 80186, 80286, 80386, and 80486
- Complex instructions that can perform multiple operations
- Variable instruction length
- Emphasis on hardware complexity for simpler compiler design
- Examples: Intel x86, AMD64 (==Advanced Micro Devices==)

### RISC (Reduced Instruction Set Computing)
- Used by ARM ==Advanced RISC Machine==, RISC-V, MIPS, PowerPC
- Simple instructions that perform single operations
- Fixed instruction length
- Emphasis on compiler optimization
- Examples: ARM Cortex series, Apple M1/M2, RISC-V

## Common Architectures

### x86 (32-bit)
- Originally developed by Intel
- Little-endian architecture
- Features:
  - Variable instruction length (1-15 bytes)
  - Complex addressing modes
  - Backward compatibility to 8086
- Register set:
  - General purpose: EAX, EBX, ECX, EDX
  - Index/pointers: ESI, EDI, ESP, EBP
  - Segment: CS, DS, SS, ES, FS, GS
  - Flags: EFLAGS

### x86_64 (AMD64)
- 64-bit extension of x86
- Introduced by AMD, later adopted by Intel
- Enhancements over x86:
  - 64-bit registers (RAX, RBX, etc.)
  - More general-purpose registers (R8-R15)
  - Larger address space (theoretically 64-bit, practically 48-bit)
  - Better SIMD support (AVX, AVX2, AVX-512)

### ARM (Advanced RISC Machine)
- Dominant in mobile/embedded devices
- Multiple versions:
  - ARMv7 (32-bit)
  - ARMv8 (64-bit/AArch64)
  - ARMv9 (Latest generation)
- Key features:
  - Load-store architecture
  - Fixed instruction length (32-bit in ARM mode)
  - Conditional execution
  - Hardware floating point (VFP)
  - SIMD instructions (NEON)


## Memory Models

### Von Neumann Architecture
- Single memory space for both data and instructions
- Characteristics:
  - Simpler design
  - Potential bottleneck (Von Neumann bottleneck)
  - More flexible memory usage

### Harvard Architecture
- Separate memory spaces for data and instructions
- Characteristics:
  - Better performance potential
  - More complex design
  - Common in microcontrollers
  - Often used in modified form (Modified Harvard Architecture)

## Major Features

### Pipelining
- Instruction stages:
  1. Fetch
  2. Decode
  3. Execute
  4. Memory access
  5. Write back
- Challenges:
  - Pipeline hazards
  - Branch prediction
  - Out-of-order execution

### Cache Hierarchy
- Typical levels:
  - L1 (separate I/D caches)
  - L2 (usually unified)
  - L3 (shared between cores)
- Cache coherency protocols:
  - MESI
  - MOESI
  - MESIF
