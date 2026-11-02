# LXNU ARM64 Soundwave Hardware and Firmware Matrix

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architecture profile: ARM64 / AArch64
Implementation target: Soundwave
Document status: Engineering foundation specification
Execution status: NOT RUN
Qualification status: NOT QUALIFIED

1. Purpose

This document defines the ARM64 profile boundary for Soundwave-based hardware and firmware support under Phase 3.

It records the required platform model, capability states, firmware and boot assumptions, and evidence boundaries for this architecture profile. It is not evidence of a running system, valid driver stack, or qualified hardware deployment.

2. Architecture profile definition

- Architecture: ARM64 / AArch64
- Platform target: Soundwave
- Assumption policy: ARM64 requirements are independent from AMD64 Ryzen and must not inherit AMD Ryzen, RDNA, XDNA, RADV, or x86 ISA assumptions.
- Firmware interface: UEFI or another explicitly documented interface
- Boot contract: must be qualified rather than assumed
- Hardware selection: vendor, SoC, board, GPU, NPU and firmware must be explicitly documented

3. Capability-state model

Use these distinct states:

Present -> Capable -> Driver available -> Runtime usable -> Validated in scope

Definitions:
- Present: hardware or feature is detected by the platform or firmware.
- Capable: the feature is expected to be supported by the vendor platform and SoC model.
- Driver available: kernel or OS driver support is present and available.
- Runtime usable: runtime and platform support are operationally available and safe for the intended workload.
- Validated in scope: the feature has been qualified under the relevant profile and evidence requirements.

No capability state may be treated as equivalent to validation.

4. Platform model

| Area | Required record | Status |
|---|---|---|
| Vendor and SoC | Explicit vendor, board and SoC selection | NOT SELECTED |
| CPU identity | ARM64 core model, core count, cache, topology | NOT RUN |
| ISA baseline | Native ARM64/AArch64 baseline | REQUIRED BASELINE |
| Optional extensions | Explicit optional-ISA or vendor-accelerator selections | NOT SELECTED |
| Firmware interface | UEFI or other documented interface | NOT RUN |
| Bootloader | Qualified handoff contract | NOT RUN |
| ACPI / Device Tree | Explicit platform representation | NOT RUN |
| Board and memory topology | Platform bus and memory layout | NOT RUN |

5. Architecture-level and optional-extension detection

The ARM64 Soundwave contract must define:
- native CPU baseline and vendor-specific feature set
- architecture extension handling and runtime detection
- any optional feature gates that are outside the base AArch64 specification
- platform power and thermal dependencies
- explicit fallback behavior when optional features are unavailable

No AMD64-specific ISA assumptions may be imposed on ARM64.

6. GPU, accelerator and NPU model

| Component | Requirement | Status |
|---|---|---|
| GPU | Vendor-specific GPU only when selected and qualified | NOT SELECTED |
| NPU | Vendor-specific NPU only when present and qualified | NOT SELECTED |
| Driver availability | Kernel/OS driver present and compatible | NOT RUN |
| Runtime usability | Accelerator runtime and scheduling capability available | NOT RUN |
| Qualification | Must be independently qualified before use | NOT QUALIFIED |
| Boot and firmware dependency | Vendor-specific firmware assumptions must be documented | NOT RUN |

The ARM64 profile must not assume RDNA, XDNA, RADV, x86 ISA semantics, or AMD-specific runtime behavior.

7. Firmware, boot, and handoff requirements

Required records:
- firmware interface and boot mode
- firmware compatibility and platform initialization state
- bootloader and handoff contract
- Limine compatibility status if used
- memory and storage initialization conditions
- power, thermal and security requirements
- runtime handoff and driver ordering, where applicable

Operating rules:
- Firmware assumptions must be recorded per board and vendor implementation.
- Boot contracts must be qualified, not assumed.
- Device tree or ACPI reporting must be explicit and architecture-specific.

Status: NOT RUN.

8. Memory, storage, power, thermal and security boundaries

Required records:
- memory topology, capacity and platform constraints
- storage controller and media model
- power policy and thermal boundaries
- secure boot or platform security state
- runtime security and isolation assumptions
- degraded operation and recovery conditions

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

This document defines the ARM64 Soundwave hardware and firmware boundary for Phase 3.

It does not claim successful runtime operation, hardware qualification, or a validated production platform.

Architecture profile: ARM64 / AArch64 Soundwave
Capability state: NOT QUALIFIED
Validation status: NOT RUN

---

LXNU — ARM64 and AMD64 profile handling must remain independent, explicit and evidence-backed.
