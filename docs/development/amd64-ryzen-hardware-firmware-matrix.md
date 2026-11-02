# LXNU AMD64 Ryzen Hardware and Firmware Matrix

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architecture profile: AMD64 / x86-64
Implementation target: Ryzen
Document status: Engineering foundation specification
Execution status: NOT RUN
Qualification status: NOT QUALIFIED

1. Purpose

This document defines the AMD64 profile boundary for Ryzen-based hardware and firmware support under Phase 3.

It records the required platform model, capability states, interface expectations, firmware and boot assumptions, and evidence boundaries for this architecture profile. It is not evidence of a running system, valid driver stack, or qualified hardware deployment.

2. Architecture profile definition

- Architecture: AMD64 / x86-64
- Platform target: AMD Ryzen
- Safe baseline: x86-64-v3
- Optional extension: x86-64-v4 only after explicit CPU feature detection and OS extended-state verification, including XCR0 and any required OS-visible state
- Assumption policy: AMD64 assumptions must not be imported into ARM64 without explicit validation.

3. Capability-state model

Use these distinct states:

Present -> Capable -> Driver available -> Runtime usable -> Validated in scope

Definitions:
- Present: hardware or feature is detected by the platform or firmware.
- Capable: the feature is expected to be supported by the platform and CPU model.
- Driver available: kernel or OS driver support is present and available.
- Runtime usable: runtime and platform support are operationally available and safe for the intended workload.
- Validated in scope: the feature has been qualified under the relevant profile and evidence requirements.

No state transition may be treated as equivalent to validation.

4. CPU and platform model

| Area | Required record | Status |
|---|---|---|
| Platform family | AMD Ryzen-class platform | NOT SELECTED |
| CPU identity | Vendor, model, stepping, package, core count, thread count | NOT RUN |
| ISA baseline | x86-64-v3 | REQUIRED BASELINE |
| Optional ISA extension | x86-64-v4 | CONDITIONAL |
| Microcode | Version and update state | NOT RUN |
| Feature detection | CPUID / OS-visible feature state | NOT RUN |
| XCR0 and OS extended state | Verified before optional v4 dispatch | NOT RUN |
| Cache and topology | Core, cache, NUMA, topology state | NOT RUN |
| Firmware interface | UEFI or explicitly documented interface | NOT RUN |

5. CPU and feature requirements

The AMD64 Ryzen contract must define:
- CPU identity, stepping and topology
- CPU feature baseline and optional feature set
- microcode version and update policy
- operating-system feature state checks before optional extended feature use
- explicit fallback behavior when required CPU features are unavailable

The default safe baseline remains x86-64-v3. x86-64-v4 execution is allowed only after validating the OS-visible feature set, including XCR0, and after confirming that the runtime and the platform can safely execute the required extensions.

6. GPU and accelerator model

| Component | Requirement | Status |
|---|---|---|
| Integrated GPU | AMD Radeon integration only when present | NOT SELECTED |
| Discrete GPU | AMD Radeon discrete device only when present | NOT SELECTED |
| Driver availability | Kernel/OS driver present and compatible | NOT RUN |
| Runtime usability | GPU runtime and scheduling capability available | NOT RUN |
| Validation status | Qualified in scope only with evidence | NOT QUALIFIED |
| NPU | AMD XDNA only when present and explicitly qualified | NOT SELECTED |

AMD Radeon, XDNA, RADV, and any GPU/NPU assumptions must remain profile-specific and must not leak into ARM64 contract documents.

7. Firmware, boot, and handoff requirements

Required records:
- firmware interface and boot mode
- bootloader and handoff policy
- Limine compatibility status, if used
- kernel handoff contract
- memory and storage initialization requirements
- power, thermal and security boundary conditions
- device and driver initialization ordering

Operating rules:
- Firmware assumptions must be recorded per board and BIOS/UEFI implementation.
- Limine compatibility must be qualified rather than assumed.
- Boot-time assumptions must not silently cover unsupported hardware.

Status: NOT RUN.

8. Memory, storage, power, thermal and security boundaries

Required records:
- memory topology and capacity
- storage controller and media type
- firmware power policy and thermal limits
- hardware security and secure boot configuration
- runtime-security and isolation assumptions
- recovery and fallback behavior during degraded mode

Status: NOT RUN.

9. Per-device evidence and qualification record

Each device or subsystem must maintain a record with:
- device identity
- capability state
- driver and runtime state
- validation evidence status
- evidence source
- qualification decision
- unresolved limitations

Evidence record policy:
- Discovery does not imply qualification.
- Runtime usability does not imply validated in scope.
- Validation remains separate from capability detection.

Status: NOT RUN.

10. Current status

This document defines the AMD64 Ryzen hardware and firmware boundary for Phase 3.

It does not claim successful runtime operation, hardware qualification, or a validated production platform.

Architecture profile: AMD64 / x86-64 Ryzen
Capability state: NOT QUALIFIED
Validation status: NOT RUN

---

LXNU — Intel/AMD and device decisions must be explicit, qualified, and evidence-backed.
