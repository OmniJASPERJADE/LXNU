# LXNU
Linux-based kernel engineering project for System-One OS. AMD64 and ARM64, XNU-inspired architecture built on upstream Linux.
LXNU

The kernel foundation of System-One.

One platform. One experience. Engineered end to end.

LXNU is an independent Linux kernel engineering project for System-One, a creator computing platform.

It applies selected XNU-inspired architectural principles to the proven Linux kernel foundation. The goal is to build a coherent, high-performance computing platform without sacrificing openness, transparency, or maintainability.

LXNU is not macOS. It is not a Mach kernel port. It contains no Mach source code or Apple code.

---

The Vision

Computing has become unnecessarily fragmented.

Operating systems often combine disconnected services, inconsistent interfaces, overlapping responsibilities, and layers of complexity that users should never have to manage.

LXNU is part of a different approach.

We believe powerful computing should feel coherent. Hardware, kernel architecture, userspace, graphics, storage, security, and applications should work together through deliberate engineering.

The freedom to build. The discipline to make it feel simple.

Architecture

LXNU uses upstream Linux as its kernel foundation.

Linux provides the established core:

- CPU architecture and hardware initialization.
- Process management and scheduling.
- Virtual memory and physical memory management.
- Virtual filesystem and filesystem infrastructure.
- Networking and device drivers.
- Interrupt handling and synchronization.

LXNU defines its own architecture, integration contracts, AMD platform policies, downstream patch management, and validation requirements.

System-One Integration

LXNU is designed to work with the wider System-One platform.

Component| Responsibility
LXNU| Kernel architecture and integration
OmniRed| Workload and resource coordination
OmniSoft| Computer AI Research Foundation
OmniSilicon| AMD hardware discovery and qualification
Omni Performance Libraries| Optimized operations and runtime dispatch
Photon| Desktop and graphical experience
OrbionFS| Unified storage orchestration

These components must use documented interfaces and clearly defined ownership boundaries.

Platform Direction

- Architectures: AMD64 (Ryzen) and ARM64 (Soundwave)
- AMD64 profile: supported AMD Ryzen processors; supported AMD Radeon GPUs where applicable; qualified AMD XDNA hardware where supported.
- ARM64 profile: native AArch64 target; SoC, graphics, accelerator, firmware, and driver selections remain explicitly unqualified until a target platform is approved.
- Kernel foundation: Upstream Linux
- Language policy: See Language Policy below.
- Optimization: Runtime-safe instruction dispatch and validated fallbacks
- Security: Linux security infrastructure with explicit policy and testing

Advanced processor instructions and hardware accelerators are enabled only when the required capabilities are detected and validated.

Language Policy

C, C++, and Rust are the only strategic implementation languages for System-One.

Language selection is determined by subsystem responsibility, ABI requirements, safety needs, operating constraints, and maintenance model.

C remains essential for Linux kernel integration, low-level interfaces, drivers, and performance-critical low-level implementation.
C++ is appropriate for orchestration, service logic, desktop and graphical integration, and performance-sensitive userspace components.
Rust is complementary and is used where memory safety, maintainability, and supported tooling justify its adoption, without replacing C or C++ wholesale.

The strategic implementation-language restriction does not prohibit ancillary scripting, configuration, build-description, test, or documentation languages where technically justified. Such languages do not become strategic implementation languages or establish ownership of platform subsystems.

No subsystem may adopt a language merely for trend or branding; engineering requirements and compatibility constraints govern the choice.

Architecture Profiles

System-One targets two first-class production architectures:

- AMD64 (Ryzen platform): x86-64-v3 baseline, optional runtime-dispatched x86-64-v4; supported AMD Ryzen processors; supported AMD Radeon GPUs where applicable; qualified AMD XDNA hardware where supported.
- ARM64 (Soundwave platform): native AArch64 target; processor, GPU, NPU, firmware, and driver selections remain explicitly unselected until an approved target platform is defined. AMD-specific assumptions do not transfer to this profile.

Architecture policy is defined once in "Multi-Architecture Profiles" (docs/architecture/architecture-profiles.md).

Documentation

- "Project Manifesto" (docs/manifesto.md)
- "Architecture Overview" (docs/architecture/overview.md)
- "Component Boundaries" (docs/architecture/component-boundaries.md)
- "Multi-Architecture Profiles" (docs/architecture/architecture-profiles.md)
- "Security Policy" (SECURITY.md)
- "Contribution Guidelines" (CONTRIBUTING.md)
- "Validation Gates" (docs/validation/gates.md)
- "Licensing and Source Provenance" (docs/licensing.md)

Development Status

<details>
<summary>Current engineering status</summary>Version: 1.6.6.2ɓ

Phase: Architecture and specification.

The repository currently establishes foundational project documentation.

The following have not been demonstrated by this repository:

- A completed LXNU kernel implementation.
- A successful reproducible kernel build.
- A validated bootable LXNU image.
- Qualified production hardware.
- Completed security validation.
- Measured performance improvements.
- A production release.

Validation gates remain NOT RUN until actual test evidence is recorded.

</details>Specified. NOT RUN. No gate measured. No component claimed to ship.

Contributing

Contributions are welcome when they strengthen the architecture, improve correctness, preserve upstream compatibility, or provide measurable engineering value.

Read "CONTRIBUTING.md" (CONTRIBUTING.md) before submitting changes.

Project Identity

LXNU is an independent System-One engineering project.

It draws inspiration from disciplined systems architecture while remaining committed to open-source foundations and transparent engineering.

Build something better. Make complexity disappear beneath the experience.

---

LXNU — The foundation of System-One.
