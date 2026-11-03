# OmniVec-II

## 1. Purpose
OmniVec-II defines the portable vector API and execution model for System-One, enabling runtime-safe dispatch across CPU vector widths and heterogeneous accelerators.

## 2. Scope and Responsibilities
- Vector API ownership
- Backend selection
- Execution contracts and fallback behavior

## 3. Architecture
OmniVec-II provides the portable abstraction across CPU SIMD instruction sets and supported acceleration backends. It remains separate from hardware-specific AMD and GPU implementation details.

## 4. Interfaces and APIs
- Vector API definitions
- Execution backend selection
- Error and fallback handling

## 5. Dependencies
- Toolchain ABI and dispatch rules
- OmniSilicon CPU discovery
- Omni Performance numerical libraries

## 6. Hardware Requirements
- 128-bit XMM/SSE support
- 256-bit YMM/AVX/AVX2 support
- Optional 512-bit ZMM/AVX-512 support
- Scalar reference implementation remains required

## 7. Data Structures and Memory Contracts
Vector operations must define memory alignment, type contracts, and backend-specific safety constraints.

## 8. Security Requirements
Runtime safety must prevent invalid feature use and preserve XSTATE and concurrency correctness.

## 9. Build and Integration
No global AVX-512 compilation and no -march=native for distributable binaries.

## 10. Testing and Validation
- Correctness tests
- Fallback validation
- XSTATE and concurrency tests

## 11. Performance Requirements
The portable vector API must dispatch efficiently and prefer validated optimized paths with benchmark-backed evidence.

## 12. Failure Handling and Fallback
Unsupported features must safely fall back to lower-width or scalar execution without silent correctness errors.

## 13. Engineering Status
Status: Specified

## 14. Implementation Roadmap
- Finalize portable API contracts
- Implement backend dispatch
- Validate under architecture and workload matrices

## 15. References
- 08-TOOLCHAIN/SIMD-ARCHITECTURE.md
- 10-VALIDATION/TEST-PLAN.md
