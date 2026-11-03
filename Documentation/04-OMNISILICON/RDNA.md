# OmniSilicon Radeon RDNA

## 1. Purpose
This document defines RDNA graphics hardware support, feature detection, and qualification criteria for System-One.

## 2. Scope and Responsibilities
- GPU capability discovery
- Radeon graphics runtime integration
- Thermal and power interactions

## 3. Architecture
Radeon hardware is treated as a qualified compute and graphics platform resource. Capability and runtime policy must be explicit.

## 4. Interfaces and APIs
- GPU driver and runtime interfaces
- Resource allocation and compute dispatch contracts
- Feature and compatibility discovery

## 5. Dependencies
- LXNU driver interfaces
- Mesa and RADV upstream integration
- Omni Performance libraries

## 6. Hardware Requirements
- Supported RDNA-class GPUs
- Explicit validation before enabling advanced graphics or compute features

## 7. Data Structures and Memory Contracts
GPU memory and scheduling contracts must remain precise and documented.

## 8. Security Requirements
Graphics and compute paths must remain memory-safe and validated against platform isolation expectations.

## 9. Build and Integration
The platform must use documented Radeon support paths and preserve upstream integration fidelity.

## 10. Testing and Validation
- Driver and runtime compatibility tests
- Compute and graphics workload validation
- Thermal and power safety checks

## 11. Performance Requirements
RDNA paths must be selected only after benchmark and validation evidence demonstrates value.

## 12. Failure Handling and Fallback
If a GPU path is unsupported or fails validation, the system must fall back to safe defaults.

## 13. Engineering Status
Status: Specified

## 14. Implementation Roadmap
- Define feature and compatibility matrix
- Validate Mesa/RADV and runtime integration
- Benchmark and qualify supported workloads

## 15. References
- 12-UPSTREAM/MESA-RADV.md
- 04-OMNISILICON/HARDWARE-QUALIFICATION.md
