# System-One Architecture: Component Boundaries and Integration Contracts

**Project:** System-One
**Architecture version:** Rev I.6 / System-One 1.6.6.2ɓ
**Document status:** Architecture specification — NOT RUN
**Scope:** System-One OS, LXNU, OmniSoft, OmniRed, OmniSilicon, Omni Performance Libraries

## 1. Purpose

This document establishes the architectural ownership, responsibilities, interfaces, and integration boundaries of the System-One platform.

System-One is an independent AMD64 Linux-based operating system and computing platform. Its architecture integrates a custom kernel engineering project, userspace software platform, workload orchestration, AMD hardware integration, and optimized performance libraries.

The objective is to establish one coherent platform without duplicating responsibilities, creating competing control systems, or introducing undocumented dependencies.

Every component must have:
- A defined responsibility.
- Explicit ownership of its interfaces.
- Documented dependencies.
- Defined inputs and outputs.
- Security and failure boundaries.
- Testable integration requirements.

No component may claim functionality owned by another component without an explicitly documented interface contract.

## 2. Platform Architecture

System-One consists of six primary architectural domains.

| Domain | Primary responsibility |
|---|---|
| System-One OS | Complete operating system integration and user experience |
| LXNU | Kernel architecture and Linux upstream integration |
| OmniSoft | Userspace platform and software runtime |
| OmniRed | Workload orchestration and resource coordination |
| OmniSilicon | AMD hardware discovery and qualification |
| Omni Performance Libraries | Optimized computational and media operations |

These domains cooperate through documented interfaces. They are not six independent operating systems or competing kernels.

## 3. System-One OS

### 3.1 Ownership

System-One OS owns the complete operating-system product architecture.

It is responsible for:
- Platform-wide architecture and integration.
- Boot and recovery experience.
- System installation and upgrades.
- System-wide security policy integration.
- Package and repository policy.
- Filesystem and storage orchestration policy.
- Desktop and graphical platform integration.
- System services and lifecycle management.
- Release engineering and hardware qualification.
- System-wide compatibility and validation.

### 3.2 Platform baseline

The production platform targets:
- AMD64 architecture.
- AMD Ryzen processors.
- AMD Radeon RDNA graphics.
- AMD XDNA neural processing units where supported.
- Linux 6.18 LTS-based kernel engineering.
- glibc userspace ABI.
- apk-tools and APK package format.
- runit service supervision.
- Limine bootloader.
- Wayland graphical environment.

The platform remains independent, with its own package repositories, release process, and integration policies.

### 3.3 Boot and storage architecture

The intended root architecture is:

- Limine bootloader.
- A/B system slots.
- dm-verity integrity verification.
- EROFS read-only lower root.
- OverlayFS writable upper layer.
- tmpfs-backed upper layer.
- OrbionFS storage orchestration.

OrbionFS coordinates storage roles and policies. It does not replace the underlying filesystem implementations.

Persistent user data and system state must remain separate from immutable system images according to the defined storage policy.

No component may bypass A/B integrity and rollback requirements.

### 3.4 Graphical platform

Photon is the System-One graphical experience.

Its intended architecture includes:
- Wayland.
- Wayfire and wlroots.
- Qt6 shell integration.
- Vulkan and RADV graphics.
- Validated AMDGPU/DRM HDR presentation.
- Photon UI HDR Human Interface Guidelines.

The compositor owns display composition and presentation. Applications must use documented platform interfaces rather than independently controlling display hardware.

## 4. LXNU

### 4.1 Ownership

LXNU owns the kernel engineering and integration architecture.

LXNU is based on upstream Linux and uses selected XNU-inspired architectural design patterns.

It is not Apple XNU, does not contain Mach source, and does not reproduce Apple's proprietary implementation.

### 4.2 Responsibilities

LXNU owns:
- Kernel source integration.
- Upstream Linux version and revision tracking.
- Downstream patch management.
- Kernel configuration policy.
- AMD64 platform integration.
- Kernel-facing interfaces and contracts.
- Kernel security integration.
- Kernel build and validation requirements.
- Versioned LXNU interfaces and ABI where applicable.

### 4.3 Upstream Linux responsibilities

Linux upstream remains responsible for its established kernel subsystems, including:
- Architecture and hardware initialization.
- Scheduling and task management.
- Virtual and physical memory management.
- VFS and filesystem infrastructure.
- Networking.
- Device drivers.
- Synchronization and core kernel primitives.

LXNU must not duplicate these systems without a documented technical requirement and architecture review.

### 4.4 Kernel scheduling boundary

Linux remains the owner of kernel scheduling mechanisms.

OmniRed may provide workload classification, resource policy, placement decisions, and coordination through supported kernel interfaces.

OmniRed must not introduce a competing scheduler or bypass Linux scheduling ownership.

### 4.5 Kernel security

LXNU integrates appropriate upstream Linux security mechanisms.

Potential mechanisms include:
- Linux Security Modules.
- Landlock.
- Lockdown.
- Yama.
- Integrity mechanisms.
- Validated BPF-based security policy.

The selection and activation of each mechanism require compatibility testing and documented security justification.

## 5. OmniSoft

### 5.1 Ownership

OmniSoft owns the System-One userspace software platform.

It is the primary software environment through which system services, runtime facilities, application integration, and platform APIs are delivered.

### 5.2 Responsibilities

OmniSoft owns:
- Userspace runtime architecture.
- System service integration.
- Application-facing platform interfaces.
- Software packaging integration.
- Runtime compatibility.
- Application lifecycle integration.
- Developer-facing platform facilities.
- Userspace hardware abstraction interfaces.
- Platform libraries and supporting utilities.

### 5.3 Application and software integration

OmniSoft provides the integration environment for the System-One application ecosystem.

This includes appropriate integration with:
- OmniWorks.
- Omni Graph.
- Symphony.
- Director's Cut.
- Other creator and productivity applications.
- System utilities and development tools.

Applications must consume documented platform APIs.

Applications must not directly assume ownership of kernel scheduling, hardware power policy, or system-wide resource allocation.

### 5.4 Runtime boundaries

OmniSoft operates above LXNU.

It must use documented kernel interfaces and userspace ABI contracts.

It must not:
- Replace kernel responsibilities with userspace imitations.
- Introduce an alternative kernel scheduler.
- Circumvent system security policy.
- Create undocumented dependencies on internal kernel structures.

## 6. OmniRed

### 6.1 Ownership

OmniRed owns workload orchestration and heterogeneous resource coordination.

Its purpose is to coordinate how eligible workloads use the available AMD CPU, GPU, and NPU resources.

### 6.2 Responsibilities

OmniRed owns:
- Workload classification.
- Resource-placement policy.
- CPU/GPU/NPU workload coordination.
- Workload prioritization.
- Resource allocation decisions through supported interfaces.
- Power and thermal coordination policy.
- Performance-policy coordination.
- Workload monitoring and feedback.
- Resource contention management.

### 6.3 Hardware execution boundary

OmniRed does not own hardware discovery or low-level device initialization.

OmniSilicon provides hardware capability information.

LXNU and upstream Linux provide the kernel mechanisms and device interfaces.

Omni Performance Libraries provide optimized computational operations.

OmniSoft provides the userspace runtime and integration environment.

OmniRed coordinates these capabilities without replacing their responsibilities.

### 6.4 Scheduling boundary

OmniRed must respect Linux kernel scheduling ownership.

Its workload placement and prioritization decisions must use supported interfaces and must not depend on undocumented kernel internals.

Any integration requiring new kernel interfaces must be reviewed and implemented through the LXNU engineering process.

## 7. OmniSilicon

### 7.1 Ownership

OmniSilicon owns AMD hardware discovery, capability reporting, and platform qualification.

It provides a consistent hardware capability model to the rest of System-One.

### 7.2 Responsibilities

OmniSilicon owns:
- AMD processor identification.
- CPU feature discovery.
- Radeon GPU capability discovery.
- RDNA architecture capability reporting.
- XDNA NPU capability discovery where supported.
- Hardware topology reporting.
- Supported device capability enumeration.
- Hardware qualification data.
- Platform compatibility reporting.

### 7.3 Hardware abstraction

OmniSilicon must distinguish between:
- Hardware presence.
- Hardware capability.
- Driver availability.
- Runtime availability.
- Validated operational support.

Discovering a device does not establish that its complete feature set is supported.

A capability must not be advertised as production-ready until its complete software and hardware execution path has been validated.

### 7.4 AMD platform requirements

The production hardware target is AMD64.

The platform prioritizes:
- AMD Ryzen CPU architectures.
- Radeon RDNA 3.5 and RDNA 4 where supported.
- AMD XDNA NPU generations where supported.
- AMDGPU and RADV integration.
- Runtime CPU instruction-set discovery.

OmniSilicon must not assume every AMD processor or GPU exposes identical capabilities.

## 8. Omni Performance Libraries

### 8.1 Ownership

Omni Performance Libraries own optimized computational and media-operation libraries used throughout System-One.

Their purpose is to provide reusable, validated, hardware-aware operations without duplicating hardware control or workload orchestration.

### 8.2 Responsibilities

The libraries may provide:
- SIMD and vector operations.
- Numeric and mathematical primitives.
- Image-processing operations.
- Compression and decompression.
- Media-processing primitives.
- Memory and data transformation operations.
- CPU/GPU/NPU execution backends where appropriate.
- Runtime-safe optimization dispatch.
- Scalar fallback implementations.

### 8.3 Runtime dispatch

The validated baseline is x86-64-v3.

Optional x86-64-v4 execution requires runtime validation of processor feature bits and operating-system extended-state support, including the relevant XCR0 state.

Unsupported instructions must never be executed through an unsafe global compiler assumption.

Every optimized path must have a compatible fallback where required.

### 8.4 Correctness and performance

Optimized implementations must preserve defined functional behavior.

Performance claims require reproducible benchmarks against a documented baseline.

Benchmarks must identify hardware, software versions, workload, measurement methodology, and results.

An optimized code path is not automatically a faster code path.

## 9. Cross-Component Integration Contracts

The primary integration relationships are:

| Provider | Consumer | Contract |
|---|---|---|
| LXNU | OmniSoft | Kernel interfaces and userspace ABI |
| LXNU | OmniRed | Supported resource and scheduling interfaces |
| LXNU | OmniSilicon | Kernel-facing hardware and device interfaces |
| OmniSilicon | OmniRed | Hardware capability and topology data |
| OmniSilicon | OmniSoft | Userspace hardware capability information |
| Omni Performance Libraries | OmniSoft | Reusable optimized operations |
| Omni Performance Libraries | OmniRed | Validated execution capabilities |
| OmniRed | OmniSoft | Workload coordination and resource-policy services |
| All domains | System-One OS | Platform integration and release contracts |

All interfaces must define:
- Ownership.
- Versioning.
- Data structures.
- Error handling.
- Permission boundaries.
- Compatibility requirements.
- Failure behavior.
- Validation requirements.

No private implementation detail should become a public interface without explicit review.

## 10. Security and Trust Boundaries

Security responsibility is distributed but must remain clearly owned.

- LXNU owns kernel-side security integration.
- OmniSoft owns userspace runtime and service security.
- OmniRed must enforce authorization and resource-policy boundaries.
- OmniSilicon must validate the provenance and reliability of hardware capability data.
- Omni Performance Libraries must validate memory safety, input handling, and execution boundaries.
- System-One OS owns platform-wide security integration and release requirements.

No component may bypass another component's security boundary through undocumented privileged access.

Privilege escalation, device access, inter-process communication, and kernel interfaces require explicit authorization.

## 11. Failure Isolation and Recovery

Components must fail within their defined ownership boundaries.

Requirements:
- Userspace service failure must not automatically imply kernel failure.
- Workload orchestration failure must not corrupt kernel scheduling state.
- Hardware capability discovery failure must not result in unsupported features being advertised.
- Library optimization failure must permit a safe fallback where applicable.
- Platform update failure must preserve the integrity of the A/B recovery mechanism.
- Component failures must produce diagnosable logs and defined error states.

System-One Health owns the user-facing recovery environment and must preserve system-slot integrity.

## 12. Dependency Direction

The intended dependency direction is:

1. LXNU provides kernel mechanisms and interfaces.
2. OmniSilicon discovers and qualifies available hardware capabilities.
3. Omni Performance Libraries implement optimized operations.
4. OmniRed coordinates eligible workloads and resources.
5. OmniSoft integrates userspace services and application facilities.
6. System-One OS integrates the complete platform and user experience.

These are logical ownership relationships, not a requirement that every operation execute in a strict serial order.

Circular dependencies between primary domains are prohibited unless an explicitly documented interface design demonstrates why they are necessary.

## 13. Change Management

Changes affecting component ownership or integration contracts require architecture review.

Every change must identify:
- Affected components.
- Interface compatibility impact.
- Security impact.
- Performance implications.
- Dependency changes.
- Migration requirements.
- Testing requirements.
- Rollback behavior.

Public or cross-component interfaces must be versioned and documented.

Unreviewed changes must not silently transfer architectural ownership.

## 14. Validation Requirements

The following validation areas must be completed before implementation or production claims are made:

| Validation area | Status |
|---|---|
| Component ownership audit | NOT RUN |
| Interface inventory | NOT RUN |
| Cross-component dependency audit | NOT RUN |
| Kernel/userspace ABI validation | NOT RUN |
| OmniRed scheduling integration | NOT RUN |
| OmniSilicon hardware qualification | NOT RUN |
| Performance library correctness | NOT RUN |
| Runtime dispatch validation | NOT RUN |
| Security boundary review | NOT RUN |
| Failure isolation testing | NOT RUN |
| Full platform integration | NOT RUN |

A written architecture is not evidence of a working implementation.

## 15. Governing Architecture Principle

System-One is engineered as one integrated platform with distinct, accountable components.

LXNU provides the kernel foundation.

OmniSoft provides the userspace software platform.

OmniRed coordinates workloads and heterogeneous resources.

OmniSilicon identifies and qualifies AMD hardware capabilities.

Omni Performance Libraries provide optimized and validated computational operations.

System-One OS integrates these domains into one complete operating system.

**One platform. Clear ownership. Explicit interfaces. Measured results.**

**Specified. NOT RUN. No gate measured. No component claimed to ship.**
