# LXNU AMD64 Platform

## 1. Purpose
This document defines the AMD64 hardware platform baseline for System-One, including CPU architecture expectations, feature detection, x86-64-v3 baseline, optional x86-64-v4 runtime dispatch, and platform-level security and driver constraints.

## 2. Scope and Responsibilities
- Define AMD64 target baseline and hardware assumptions
- Specify feature gates and validation requirements
- Coordinate with toolchain, OmniSilicon, and validation

## 3. Architecture
System-One targets AMD64 as the primary production platform. The architecture baseline is x86-64-v3, with optional runtime-dispatched x86-64-v4 execution enabled only after explicit validation.

## 4. Interfaces and APIs
- CPUID feature discovery
- XCR0 validation
- ABI contracts for toolchain and kernel integration
- Driver feature gate interfaces

## 5. Dependencies
- Toolchain definitions
- OmniSilicon hardware discovery
- Validation and benchmark environment

## 6. Hardware Requirements
- AMD64-capable Ryzen-class systems
- 128-bit, 256-bit, optional 512-bit CPU vector support by policy
- Feature-subset validation before optimization enablement

## 7. Data Structures and Memory Contracts
The platform must not assume vector widths without explicit detection and safe fallback. ABI and memory alignment for vectorized code must remain explicit.

## 8. Security Requirements
- No unsafe assumption of instruction support
- Feature enablement must follow validation and gating
- Kernel and user-space runtime must reject invalid feature combinations

## 9. Build and Integration
- No global AVX-512 compilation
- No -march=native for distributable binaries
- Use explicit feature selection and runtime dispatch

## 10. Testing and Validation
- CPU feature validation at boot or runtime
- XSTATE and fallback policy testing
- Concurrency and multithreaded validation

## 11. Performance Requirements
The runtime must prefer validated feature paths and preserve scalar fallback correctness.

## 12. Failure Handling and Fallback
If the CPU does not support a target vector mode, the runtime must fall back to a supported baseline rather than failing eagerly.

## 13. Engineering Status
Status: Specified

## 14. Implementation Roadmap
- Define baseline CPU and feature models
- Validate CPUID/XCR0 policy
- Complete toolchain and SIMD dispatch integration
- Validate hardware qualification and performance benchmarks

## 15. References
- 08-TOOLCHAIN/SIMD-ARCHITECTURE.md
- 04-OMNISILICON/RYZEN.md
- 10-VALIDATION/TEST-PLAN.md
