# LXNU Kernel and Userspace ABI Boundary Specification

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Document status: Engineering foundation specification
Execution status: NOT RUN

1. Purpose

This document defines the kernel-to-userspace boundary for LXNU and System-One OS. The purpose is to establish explicit ABI contracts before subsystem implementation begins, so that userspace services, orchestration layers, and platform services do not depend on hidden kernel internals.

2. Architectural Rule

The kernel boundary is owned by LXNU.

The userspace service boundary is owned by System-One OS.

A subsystem may consume kernel services only through the documented ABI and supported contract surface. Kernel internals remain private unless they are formally reviewed, versioned, and exposed as a supported interface.

3. Ownership Boundary

| Layer | Owner | Responsibility |
|---|---|---|
| Kernel | LXNU | Scheduling, memory model, process model, device interfaces, kernel ABI |
| Userspace services | System-One OS | Service lifecycle, runtime compatibility, userspace orchestration, platform integration |
| Workload orchestration | OmniRed | Policy execution and placement requests using supported interfaces |
| Hardware discovery | OmniSilicon | Capability reporting and validated hardware model |

4. Required ABI Contract Elements

Every kernel-facing or userspace-facing API must define:
- owner and maintenance authority
- version number
- accepted inputs
- output forms and data contracts
- error handling semantics
- privilege and authorization requirements
- compatibility and deprecation policy
- architecture-specific behavior
- validation and test expectations

5. Kernel Interface Categories

### 5.1 Syscall and kernel service boundary

The boundary must define:
- supported syscall surface
- compatibility policy on argument semantics
- data ownership and pointer validity rules
- requirement for userspace-safe memory access
- failure semantics and errno semantics

### 5.2 Device interfaces

Kernel device discovery and driver interfaces must be defined by LXNU and the selected platform contract.

Requirements:
- no direct userspace ownership of kernel device state
- no implicit accelerator assumptions across profiles
- clear driver availability and runtime-availability distinctions

### 5.3 Resource and scheduling interfaces

OmniRed may request scheduling, policy, and resource-placement information through supported interfaces.

LXNU remains the authoritative owner of scheduler behavior and kernel resource management.

6. Userspace Runtime Contract

System-One OS owns the runtime contract for services and applications.

Required elements:
- process lifecycle policies
- service supervision model
- configuration and data ownership
- boot integration
- application compatibility assumptions
- runtime fallback behavior

The userspace runtime contract must not assume direct ownership of kernel scheduling, privileged memory policy, or low-level accelerator control.

7. AMD64 and ARM64 ABI Rules

The public ABI contract must remain architecture-neutral at the interface boundary, while architecture-specific behavior is recorded explicitly in metadata.

Rules:
- AMD64 and ARM64 must not share the same undocumented instruction assumptions.
- Syscall semantics and data layout must be checked per profile.
- Architecture-specific extensions must be represented as explicit capability records.
- No architecture profile may inherit handling assumptions from the other without a documented contract.

8. Security and Trust Boundary

Kernel userspace boundaries must include:
- least-privilege access rules
- authorization checks for privileged operations
- explicit error isolation for privileged failures
- no cross-subsystem bypass of privilege controls

No subsystem may rely on implicit trust between userspace and kernel layers.

9. Validation Gates

Before implementation proceeds, the ABI contract must be checked for:
- ownership clarity
- data contract completeness
- compatibility strategy
- profile-specific behavior
- failure semantics
- security boundary correctness

Status: NOT RUN.

10. Current Status

This document defines the required kernel and userspace boundary contract for Phase 3. It is not evidence of implementation, boot success, or runtime validation.

Specified. NOT RUN. No gate measured. No component claimed to ship.
