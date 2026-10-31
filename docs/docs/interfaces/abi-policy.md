LXNU Interface and ABI Stability Policy

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architectures: AMD64 (Ryzen), ARM64 (Soundwave)
Status: Engineering specification
Execution status: NOT RUN

1. Purpose

This policy defines how LXNU identifies, versions, documents, and maintains interfaces used by the Linux kernel and System-One components.

It establishes clear boundaries between upstream Linux interfaces, LXNU-owned interfaces, and userspace application binary interfaces.

The purpose is to prevent accidental compatibility promises and uncontrolled coupling between components.

Interfaces are defined per target architecture. AMD64 uses x86_64-linux-gnu; ARM64 uses aarch64-linux-gnu. ABI guarantees, structure layouts, and calling conventions are documented per architecture and are not assumed identical. An architecture-specific interface extension requires review under the same rules as any other interface change.

2. Interface Principles

LXNU interfaces must follow these principles:

- Prefer established upstream Linux interfaces.
- Avoid unnecessary private kernel interfaces.
- Keep kernel and userspace responsibilities separate.
- Define ownership for every LXNU-specific interface.
- Document compatibility expectations.
- Version intentional interface changes.
- Preserve backward compatibility where explicitly promised.
- Never claim ABI stability before the interface is reviewed and frozen.

3. Interface Categories

Category| Description
Upstream kernel ABI| Existing Linux userspace interfaces
Kernel internal API| Internal interfaces subject to upstream change
LXNU kernel interface| Explicitly maintained LXNU-specific kernel interface
Userspace ABI| Binary compatibility contract for userspace
Userspace API| Source-level interface for applications and libraries
IPC interface| Communication between independent processes
Hardware interface| Standard kernel interfaces used to access hardware
Build interface| Contracts between source, configuration, and build tooling

These categories must not be treated as interchangeable.

4. Ownership

Interface ownership must follow subsystem responsibility.

Component| Interface responsibility
Upstream Linux| Core kernel interfaces and established kernel ABI
LXNU| Kernel integration contracts and justified LXNU-specific interfaces
OmniRed| Workload coordination and resource-policy interfaces
OmniSilicon| Hardware discovery and capability-reporting interfaces
OmniSoft| Userspace runtime and platform integration
Omni Performance Libraries| Optimized operation and dispatch interfaces
Photon| Desktop shell and compositor-facing integration
System-One| Platform-wide compatibility policy

No component may silently assume ownership of another component's interface.

5. Linux Compatibility

LXNU must preserve compatibility with established upstream Linux userspace interfaces wherever practical.

It must not unnecessarily break:

- System calls.
- Standard device interfaces.
- Established filesystem interfaces.
- Networking interfaces.
- Process and memory-management behavior.
- Existing userspace application expectations.

Any required incompatibility must be documented with technical justification and migration guidance.

6. LXNU-Specific Interfaces

LXNU-specific interfaces must be introduced only when an actual architectural requirement cannot be met adequately through existing upstream interfaces.

Each interface must document:

1. Interface name and identifier.
2. Owning subsystem.
3. Purpose.
4. Input and output definitions.
5. Data structures and field semantics.
6. Error handling.
7. Permission and security requirements.
8. Versioning rules.
9. Compatibility expectations.
10. Validation requirements.

Private interfaces must not be exposed as stable public contracts by accident.

7. ABI Versioning

An ABI version must identify an intentional compatibility contract.

Changes should be classified as:

- Compatible: Existing consumers continue to function without modification.
- Additive: New functionality is introduced without invalidating existing consumers.
- Breaking: Existing consumers may require modification.
- Deprecated: An interface remains available but is scheduled for retirement.
- Removed: An interface is no longer supported.

Breaking changes require explicit review, migration documentation, and an appropriate versioning decision.

8. Version and Compatibility Policy

The LXNU architectural baseline is 1.6.6.2ɓ.

This project version does not automatically establish a frozen kernel ABI.

ABI versioning must remain separate from project release numbering.

An interface may be declared stable only after:

- Ownership is assigned.
- Its specification is complete.
- Compatibility requirements are approved.
- Tests cover its required behavior.
- Security implications are reviewed.
- A maintenance commitment exists.

9. Kernel Internal Interfaces

Linux kernel internal APIs are not automatically stable across upstream kernel revisions.

LXNU must avoid exposing internal kernel implementation details as permanent userspace contracts.

Downstream modifications to internal APIs must be tracked in the patch inventory and reviewed during upstream synchronization.

10. IPC and Userspace Contracts

Communication between System-One components must use documented contracts.

Where applicable, interface specifications must define:

- Message formats.
- Serialization rules.
- Version negotiation.
- Permissions.
- Failure behavior.
- Resource limits.
- Compatibility expectations.

IPC must not become an undocumented dependency between independently maintained components.

11. Security Requirements

Interface design must consider:

- Input validation.
- Authorization.
- Privilege boundaries.
- Memory safety.
- Information disclosure.
- Resource exhaustion.
- Race conditions.
- Version negotiation abuse.

Interfaces must expose only the capabilities required by their intended consumers.

12. Deprecation and Removal

An established interface must not be removed without review.

Deprecation records must identify:

- Reason for deprecation.
- Affected consumers.
- Replacement interface, if available.
- Migration requirements.
- Expected removal conditions.

Security-critical changes may require accelerated removal, with the rationale documented.

13. Validation

Interface validation must include applicable:

- Specification review.
- ABI compatibility testing.
- API tests.
- Error-path tests.
- Permission tests.
- Cross-version compatibility tests.
- Regression tests.
- Security review.

A written interface specification alone does not establish working compatibility.

14. Current Status

This document defines the intended LXNU interface and ABI policy.

The LXNU ABI is not declared frozen or production-stable by this document.

No completed LXNU-specific ABI implementation, compatibility test suite, or production compatibility guarantee is claimed.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Stable contracts. Deliberate evolution. No accidental promises.