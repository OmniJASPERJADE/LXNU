# System-One Architecture

## 1. Purpose
This document defines the top-level architecture and subsystem boundaries for System-One. It is the primary governance document for the documentation tree and is intended to be read alongside the master specification and engineering status register.

## 2. Organization hierarchy
System-One is organized as a layered and explicitly bounded platform:

1. Platform governance
2. Kernel and CPU baseline
3. Userspace runtime and platform services
4. Resource coordination and recovery
5. Compute acceleration and heterogeneous execution
6. Storage and integrity management
7. Desktop user experience
8. Toolchain and build system
9. Distribution and deployment
10. Validation and qualification
11. Development infrastructure
12. Upstream policy and integration

## 3. Architecture tree
- 00-MASTER: master docs and governance
- 01-LXNU: kernel and platform baseline
- 02-OMNISOFT: userspace API surface and application integration
- 03-OMNIRED: orchestration, services, and recovery
- 04-OMNISILICON: AMD hardware qualification and accelerator discovery
- 05-OMNI-PERFORMANCE: tuned compute libraries and runtime dispatch
- 06-ORBIONFS: filesystem and integrity policy
- 07-PHOTON: desktop environment and visual design
- 08-TOOLCHAIN: compiler, ABI, and vector dispatch policy
- 09-DISTRIBUTION: boot, package management, and updates
- 10-VALIDATION: workloads and qualification
- 11-DEVELOPMENT-INFRASTRUCTURE: distributed build environment
- 12-UPSTREAM: cross-project integration strategy

## 4. Execution and data flow
The platform is intended to route data from hardware discovery through kernel initialization, runtime coordination, application execution, storage I/O, and validation evidence capture. Each subsystem must expose explicit contracts and not rely on implicit behavior.

## 5. Status and traceability
Architecture and policy decisions are recorded at the top level. Implementation details live in subsystem docs. Validation status is captured separately to preserve the distinction between design and evidence.

## 6. References
- SYSTEM-ONE-MASTER-SPEC.md
- ENGINEERING-STATUS.md
- ROADMAP.md
