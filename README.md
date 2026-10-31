# LXNU
Linux-based kernel engineering project for System-One OS. AMD64 and ARM64, XNU-inspired architecture built on upstream Linux.
LXNU

The kernel foundation of System-One.

One platform. One experience. Engineered end to end.

LXNU is an independent Linux kernel engineering project for System-One, a creator computing platform.

It applies selected XNU-inspired architectural principles to the proven Linux kernel foundation. The goal is to build a coherent, high-performance computing platform without sacrificing openness, maintainability, or technical transparency.

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
OmniSoft| Userspace platform and runtime
OmniSilicon| AMD hardware discovery and qualification
Omni Performance Libraries| Optimized operations and runtime dispatch
Photon| Desktop and graphical experience
OrbionFS| Unified storage orchestration

These components must use documented interfaces and clearly defined ownership boundaries.

Platform Direction

- Architectures: AMD64 (Ryzen) and ARM64 (Soundwave)
- CPU: Supported AMD Ryzen processors
- Graphics: Supported AMD Radeon GPUs
- AI acceleration: Qualified AMD XDNA hardware
- Kernel foundation: Upstream Linux
- Languages: C, C++, and stable Rust where appropriate
- Optimization: Runtime-safe instruction dispatch and validated fallbacks
- Security: Linux security infrastructure with explicit policy and testing

Advanced processor instructions and hardware accelerators are enabled only when the required capabilities are detected and validated.

Engineering Principles

1. Integration over fragmentation — components must work together through defined contracts.
2. Measured performance — no speedup claims without reproducible benchmarks.
3. Security by design — security requirements belong in architecture and implementation.
4. Upstream respect — preserve Linux provenance, licensing, and maintainability.
5. Minimal justified complexity — every subsystem must earn its place.
6. Evidence before release — specifications, implementation, testing, and verification are distinct stages.

Architecture Profiles

System-One targets two first-class production architectures:

- AMD64 (Ryzen platform): x86-64-v3 baseline, optional runtime-dispatched x86-64-v4.
- ARM64 (Soundwave platform): native AArch64 target; processor, GPU, and NPU vendors are not yet selected.

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