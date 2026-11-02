# LXNU Phase 3: Subsystem Interface and Dependency Contract

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architecture profiles: AMD64 (Ryzen) and ARM64 (Soundwave)
Document status: Engineering foundation specification
Execution status: NOT RUN

1. Purpose

This document defines the initial engineering contract for the Phase 3 foundation stage.

It establishes the minimum set of subsystem interfaces, dependency boundaries, and ownership rules required before implementation work begins. The objective is to prevent uncontrolled coupling, undocumented kernel/userspace assumptions, and cross-profile hardware assumptions before code is written.

This document does not claim an implementation, successful build, boot result, hardware qualification, or production validation.

2. Scope

This contract applies to the System-One platform architecture and the LXNU engineering foundation.

In scope:
- LXNU kernel and userspace boundary.
- System-One OS service and runtime boundary.
- OmniRed workload orchestration and resource policy boundary.
- OmniSilicon hardware capability and qualification boundary.
- OmniSoft AI research and computational runtime boundary.
- Omni Performance Libraries ABI and dispatch boundary.
- AMD64 and ARM64 profile-specific implementation boundaries.

Out of scope:
- Product-specific UI or app implementation details.
- Detailed device-driver implementations.
- Performance benchmark claims.
- Production release readiness.

3. Governing Principles

The following principles are mandatory for all interfaces defined in this document:

- Clear ownership.
- Explicit inputs and outputs.
- Documented versioning and compatibility rules.
- Architecture-neutral public contracts.
- Profile-specific capability records for AMD64 and ARM64.
- No undocumented access to internal kernel state.
- No ownership transfer through implicit coupling.
- Failure behavior must be defined and diagnosable.
- Security and least-privilege boundaries must be explicit.

4. Subsystem Ownership Summary

| Subsystem | Primary ownership |
|---|---|
| LXNU | Kernel architecture, Linux upstream integration, kernel-facing interfaces, validation contract |
| System-One OS | General userspace integration, system services, runtime compatibility, release and platform integration |
| OmniSoft | AI research and computational research environment, AI runtime infrastructure, research execution services |
| OmniRed | Workload classification, resource placement, orchestration policies, power and thermal coordination |
| OmniSilicon | Hardware discovery, capability reporting, qualification, and profile-specific hardware model |
| Omni Performance Libraries | Optimized computational operations, runtime dispatch, fallback correctness |
| Photon / OrbionFS / other platform services | Their documented service interfaces and platform responsibilities as separately defined |

All subsystems must operate through documented contracts and must not claim ownership of responsibilities assigned to another domain.

5. Dependency Direction

The dependency direction is intentionally one-way for architectural ownership:

1. LXNU provides kernel mechanisms and interfaces.
2. OmniSilicon provides capability and platform qualification data.
3. Omni Performance Libraries provide validated optimized operations.
4. OmniRed coordinates workload placement and policy execution.
5. System-One OS integrates general userspace services, application compatibility, and platform services.
6. OmniSoft provides AI research and computational research runtime facilities and AI-specific services.

This order defines ownership and governance. It does not require execution to be strictly serial at runtime, but it does require that architectural dependency boundaries remain explicit and reviewable.

6. Interface Contract Model

Every subsystem interface must define the following:

- Owner and maintenance authority.
- Interface name and version.
- Accepted input types and data contracts.
- Required outputs and error codes.
- Permission and authorization boundaries.
- Failure mode and rollback behavior.
- Compatibility rules across subsystem versions.
- Validation gate and test expectations.
- Architecture profile applicability.

A private implementation detail must not become a public interface without explicit review.

7. Kernel and Userspace Boundary

### 7.1 LXNU to System-One OS

LXNU owns the kernel boundary and kernel-facing interfaces.

System-One OS owns the userspace service boundary and system-level integration.

Required contract elements:
- userspace ABI definition
- kernel API or syscall boundary definition
- data structure compatibility rules
- error propagation and policy handling
- userspace boot and service lifecycle integration
- security boundary and privilege model

Requirements:
- No userspace subsystem may depend on internal kernel structures.
- No kernel subsystem may silently assume a service layer owns privileged policy decisions.
- ABI differences between AMD64 and ARM64 must be documented separately.

### 7.2 LXNU to OmniRed

OmniRed may request scheduling and resource-policy information through supported kernel interfaces.

LXNU owns the kernel scheduling boundary and the validity of kernel-facing interfaces.

Requirements:
- OmniRed must not bypass the kernel scheduler.
- OmniRed must not define a competing scheduler.
- Resource placement decisions must remain policy-driven and interface-mediated.

### 7.3 LXNU to OmniSilicon

OmniSilicon provides hardware discovery and capability information.

LXNU owns the kernel-facing hardware interfaces and kernel integration paths.

Requirements:
- Capability discovery must be explicit and qualified.
- Unsupported features must not be advertised as available.
- Architecture-specific discovery results must remain profile-specific.

8. System-One OS Interface Boundary

System-One OS is responsible for the general platform boundary, service lifecycle, runtime compatibility, and user-facing platform coordination.

Key contract areas:
- service supervision and lifecycle management
- package and repository policy
- boot and recovery policy integration
- userspace runtime compatibility
- application-facing platform API boundaries
- general system security and release policy

System-One OS must not claim responsibility for AI research runtime boundaries, workload orchestration policy, or low-level hardware qualification unless explicitly assigned and documented.

9. OmniSoft Interface Boundary

OmniSoft owns the AI research and computational research runtime environment.

This boundary must define:
- AI runtime execution interfaces
- research-service integration boundaries
- model execution and environment contracts
- hardware execution backend negotiation
- userspace runtime compatibility and dependencies
- safe fallback and error handling behavior

OmniSoft must not directly own general OS service lifecycle, general application integration, or kernel scheduling policy.

10. OmniRed Interface Boundary

OmniRed owns workload orchestration and heterogeneous resource coordination.

Required contract areas:
- workload classification metadata
- placement policy interfaces
- CPU/GPU/NPU scheduling decisions by policy
- performance and thermal policy boundaries
- resource contention and monitoring signals
- conflict handling with kernel scheduling ownership

Requirements:
- OmniRed is not a replacement for Linux scheduling.
- OmniRed must operate through supported interfaces only.
- Policy decisions must be auditable and compatible with the current kernel contract.

11. OmniSilicon Interface Boundary

OmniSilicon owns hardware capability discovery and platform qualification.

This boundary must define:
- processor and accelerator discovery
- capability classification model
- driver availability and runtime availability states
- validated support state
- architecture-specific model for AMD64 and ARM64
- failure and unknown-state reporting

Required capability states:
1. Present
2. Capable
3. Driver available
4. Runtime usable
5. Validated in scope

A capability must not be reported as usable until the relevant validation path is evidence-backed.

12. Omni Performance Libraries Interface Boundary

Omni Performance Libraries own optimized computational operations and dispatch behavior.

Required contract areas:
- ABI and symbol-level compatibility
- runtime dispatch policy
- supported instruction-set baseline
- safe scalar fallback behavior
- arithmetic and memory correctness guarantees
- error handling for unsupported instructions or missing state

Requirements:
- Unsupported code paths must never execute due to unsafe compiler assumptions.
- All optimized paths require a documented fallback or safe failure mode.
- AMD64 and ARM64 dispatch rules must remain independent and architecture-specific.

13. Cross-Profile Policy Requirements

AMD64 and ARM64 are both production targets. The same engineering model applies to both profiles, but the implementation details must remain profile-specific.

Required cross-profile rules:
- Architecture-specific capability records are explicit, not implicit.
- No AMD-specific assumption may be treated as valid on ARM64.
- No ARM64-specific assumption may be treated as valid on AMD64.
- Boot, firmware, feature detection, and accelerator assumptions must be documented per profile.
- Cross-component interfaces must be neutral in public form and explicit in architecture-specific data.

14. Validation Contract for Interfaces

Every interface must be validated at the relevant stage of implementation.

At minimum, each interface must document:
- owner
- version
- compatibility rules
- validation method
- failure handling
- security boundary
- dependency boundary
- applicable architecture profile

Interface validation gates at a minimum:
- API or ABI contract review
- dependency review
- security boundary check
- compatibility and rollback review
- architecture-specific validation for each profile

An interface is not accepted merely because it is documented; it must be demonstrated through review and validation evidence.

15. Implementation Readiness Standard

Before implementation begins, the subsystem contract must satisfy the following:

- Defined owner
- Defined responsibility boundary
- Documented dependencies
- Security and privilege model
- Error handling and rollback path
- Test strategy and validation gate
- Compatibility and versioning plan
- Profile-specific applicability defined

If these are not defined, the subsystem is not ready for implementation.

16. Phase 3 Deliverables

The immediate Phase 3 output should include the following documents, each created as a distinct engineering specification:

1. Subsystem interface and dependency contract (this document)
2. Kernel and userspace ABI boundary specification
3. System-One OS runtime and service interface specification
4. OmniRed orchestration contract
5. OmniSilicon capability discovery and qualification contract
6. OmniSoft AI runtime boundary specification
7. Omni Performance Libraries dispatch and fallback contract
8. Profile-specific hardware and firmware boundary matrices for AMD64 and ARM64

This document represents the first gate for Phase 3 and should be treated as the foundation for those follow-on engineering contracts.

17. Current Status

This document defines the required engineering foundation for Phase 3. It is not a claim that implementation has begun, that a kernel build is complete, or that any subsystem has been validated.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Engineering before implementation. Interfaces before code.
