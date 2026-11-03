# SIMD Architecture

## 1. Purpose
This document defines the CPU SIMD architecture for System-One, including register widths, instruction families, runtime safety, and fallback behavior.

## 2. Scope and Responsibilities
- ISA widths and register modeling
- instruction family and feature-subset policy
- runtime validation and safe dispatch

## 3. Architecture
System-One supports 128-bit XMM/SSE, 256-bit YMM/AVX/AVX2, and optional 512-bit ZMM/AVX-512. These decisions must remain explicitly separate from RDNA Wave32/Wave64 and XDNA vector/tile execution semantics.

## 4. Interfaces and APIs
- CPUID detection
- XCR0 validation
- runtime dispatch APIs
- scalar fallback interfaces

## 5. Dependencies
- AMD64 platform baseline
- OmniVec-II and toolchain integration
- validation test plan and benchmark evidence

## 6. Hardware Requirements
- 128-bit XMM/SSE support
- 256-bit YMM/AVX/AVX2 support
- optional 512-bit ZMM/AVX-512 support
- scalar reference implementation
- x86-64-v3 production baseline
- optional runtime-dispatched x86-64-v4

## 7. Data Structures and Memory Contracts
Vector register usage must define alignment, ownership, and safety semantics. SIMD decisions are not equivalent to GPU wave or tile semantics.

## 8. Security Requirements
Independent AVX-512 feature-subset detection is required. No global AVX-512 compilation is permitted, and no -march=native is allowed for distributable binaries.

## 9. Build and Integration
The system must compile safe, validated code paths and let the runtime decide what is actually available.

## 10. Testing and Validation
- CPUID and XCR0 validation
- XSTATE and concurrency testing
- fallback and correctness testing under all supported widths

## 11. Performance Requirements
Optimized paths must be selected only after measured performance evidence on real Ryzen hardware.

## 12. Failure Handling and Fallback
If the CPU or runtime cannot safely support an instruction set, execution falls back to a lower-width or scalar path.

## 13. Engineering Status
Status: Specified

## 14. Implementation Roadmap
- finalize SIMD policy and dispatch boundaries
- validate hardware detection and fallback rules
- confirm runtime and benchmark evidence on real systems

## 15. References
- 04-OMNISILICON/RYZEN.md
- 05-OMNI-PERFORMANCE/OMNIVEC-II.md
- 10-VALIDATION/TEST-PLAN.md
