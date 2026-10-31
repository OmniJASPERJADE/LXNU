LXNU Kernel Security Policy

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architecture: AMD64
Status: Engineering specification
Execution status: NOT RUN

1. Purpose

This document defines the security architecture and engineering requirements for the LXNU kernel.

LXNU uses upstream Linux security mechanisms and carefully controlled integration policies. Its security model must protect system integrity, isolate workloads, restrict unauthorized access, and preserve recoverability.

Security features must be validated in the running system before their effectiveness is claimed.

2. Security Principles

LXNU security engineering follows these principles:

- Minimize kernel attack surface.
- Apply least privilege.
- Prefer upstream Linux security mechanisms.
- Separate policy ownership from mechanism implementation.
- Fail closed when security decisions cannot be verified.
- Validate inputs at trust boundaries.
- Protect kernel and userspace interfaces.
- Preserve security-relevant audit evidence.
- Avoid unnecessary privileged services.
- Never equate a configured security option with effective protection.

3. Threat Model

The security design must consider:

- Malicious or compromised userspace applications.
- Privilege escalation attempts.
- Unauthorized device access.
- Malicious or vulnerable kernel modules.
- Malformed system calls and device requests.
- Memory corruption and concurrency defects.
- Compromised build dependencies.
- Tampered kernel or system images.
- Unauthorized configuration changes.
- Resource exhaustion and denial of service.
- Compromised workloads interacting with shared hardware.

The threat model must be updated as new components and interfaces are introduced.

4. Security Boundaries

The architecture must define and enforce boundaries between:

- Unprivileged applications and privileged services.
- Userspace and kernel space.
- Kernel subsystems and device drivers.
- Workloads and shared hardware resources.
- System administration and ordinary user activity.
- Verified system images and writable persistent storage.
- Build infrastructure and published artifacts.

Each boundary must have an identifiable enforcement mechanism and validation procedure.

5. Linux Security Mechanisms

LXNU intends to use established upstream Linux security facilities where appropriate.

5.1 Linux Security Modules

LSM provides kernel security hooks for supported security mechanisms.

LXNU must preserve upstream LSM functionality and document any downstream changes.

5.2 Landlock

Landlock is intended to provide application-level restrictions through supported Linux interfaces.

Policies must be tested for correct enforcement and failure behavior.

5.3 Lockdown

Kernel lockdown is intended to restrict operations that could compromise kernel integrity.

Its configuration and interaction with firmware, debugging, and privileged interfaces must be documented.

5.4 Yama

Yama provides additional restrictions for selected process-interaction operations.

Its policy must be evaluated against debugging and development requirements.

5.5 Integrity Controls

Kernel and system integrity facilities must be evaluated for compatibility with the intended boot and artifact-verification model.

5.6 BPF Security Policy

BPF-related security controls may be used where justified.

Verifier behavior, privilege requirements, program loading, attachment permissions, and policy failure modes must be reviewed.

6. Privilege and Administration

The intended System-One administration model uses:

- "doas" for controlled privilege elevation.
- "shadow" for account and authentication management.
- Minimal privileged services.
- Explicit service ownership and permissions.

LXNU must not introduce unnecessary privilege-management mechanisms or duplicate existing Linux authorization functionality.

Privileged operations must be auditable and restricted to authorized users and services.

7. Kernel Module Security

Kernel module policy must define:

- Which modules are permitted.
- How modules are sourced.
- How module integrity is verified.
- Whether module signing is required.
- How unsigned or untrusted modules are handled.
- How module-loading privileges are controlled.

A module must not be considered trusted merely because it compiles.

8. Memory and Concurrency Safety

Kernel engineering must account for:

- Buffer boundaries.
- Integer overflow and underflow.
- Use-after-free defects.
- Double-free defects.
- Race conditions.
- Reference-counting errors.
- Lock ordering and deadlocks.
- Untrusted pointer handling.
- DMA and device-memory isolation.

Rust may be used for suitable components, but it does not eliminate the need for security review.

C and C++ code must receive appropriate static analysis, review, and testing.

Unsafe Rust must have documented justification and review.

9. AMD Platform Security

AMD platform integration must account for:

- CPU security capabilities.
- Firmware security configuration.
- IOMMU and DMA isolation.
- PCIe device trust boundaries.
- GPU and NPU device access.
- Firmware and microcode provenance.
- Hardware-assisted security features where supported.

Hardware security capabilities must be detected and tested rather than assumed.

10. Verified Boot and System Integrity

System-One integration is intended to use:

- Limine boot management.
- Verified system images.
- dm-verity.
- EROFS read-only system content.
- OverlayFS with a controlled writable layer.
- A/B system deployment and rollback.

LXNU must preserve compatibility with this architecture.

The existence of these design requirements does not establish that verified boot or rollback is implemented or operational.

11. Security Updates

Security maintenance must include:

- Upstream Linux vulnerability monitoring.
- Relevant security advisories.
- Patch applicability review.
- Dependency and toolchain review.
- Rebuild requirements.
- Regression testing.
- Release documentation.

Critical security fixes must receive priority assessment.

Unresolved critical vulnerabilities must block applicable production release approval.

12. Security Testing

Security validation must include applicable:

- LSM policy tests.
- Landlock enforcement tests.
- Privilege-boundary tests.
- Module-loading policy tests.
- Kernel configuration review.
- Memory-safety analysis.
- BPF policy tests.
- Device isolation tests.
- Boot integrity tests.
- Recovery and rollback tests.
- Vulnerability scanning.
- Regression testing.

Every result must be linked to the exact source revision and configuration.

13. Failure Handling

Security-sensitive failures must not silently grant additional privileges.

Where a security mechanism cannot establish a required condition, the system must follow a documented fail-closed policy unless an explicitly approved recovery path applies.

Failures must be logged without exposing secrets or sensitive data.

14. Security Review and Release Blocking

Security review is mandatory for changes affecting:

- Privilege boundaries.
- Kernel interfaces.
- Device access.
- Memory management.
- Module loading.
- Boot integrity.
- Authentication or authorization.
- LSM and BPF policy.
- Cryptographic operations.

Unresolved critical findings block applicable release approval.

Exceptions require documented risk acceptance and approval.

15. Current Security Status

This document defines the intended LXNU kernel security policy.

No completed security implementation, security certification, penetration-test result, or production security assurance is claimed.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Security must be designed, enforced, and proven.