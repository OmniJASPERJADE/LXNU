LXNU AMD Hardware Support Matrix

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architecture: AMD64
Status: Hardware support specification
Qualification status: NOT RUN

1. Purpose

LXNU is designed for AMD-based computing systems.

This document defines the intended hardware support scope, capability discovery requirements, architecture policies, and qualification criteria.

Hardware inclusion in this document does not establish that a device has been tested, qualified, or supported in a production release.

Targeted hardware is not the same as verified hardware.

2. Platform Policy

The production platform is AMD64.

The project targets:

- AMD Ryzen processors.
- AMD Radeon RDNA graphics processors.
- AMD XDNA neural processing units.
- AMD platform controllers and associated supported devices.

Intel-targeted, ARM, PowerPC, and NVIDIA production platforms are outside the defined LXNU target.

Linux upstream remains responsible for established processor architecture support, drivers, memory management, and hardware initialization.

LXNU adds platform integration, capability reporting, qualification policy, and validation.

3. CPU Support

Zen 4 — AMD Family 19h

Target processor families include:

- Phoenix.
- Hawk Point.

The exact processor model, stepping, supported features, firmware, and platform configuration must be identified before qualification.

Zen 5 — AMD Family 1Ah

Target processor families include:

- Strix Point.
- Strix Halo.
- Gorgon Point.
- Gorgon Halo.

The exact processor model and available capabilities must be detected at runtime.

Family identification alone is insufficient to establish feature support.

4. CPU Instruction Policy

The baseline userspace target is x86-64-v3.

Advanced instruction sets require runtime-safe dispatch.

AVX-512 execution requires verification of:

- AVX-512F.
- AVX-512BW.
- AVX-512CD.
- AVX-512DQ.
- AVX-512VL.
- Required XCR0 extended-state bits 5, 6, and 7.

Hardware feature detection must be combined with operating-system state validation.

No blanket "-march=znver5" compilation policy is permitted.

Every optimized implementation must retain an appropriate fallback path.

5. Radeon Graphics Support

The intended graphics qualification scope includes supported AMD RDNA devices associated with these GPU architecture identifiers:

- gfx1100.
- gfx1103.
- gfx1150.
- gfx1151.
- gfx12xx.

These identifiers establish an engineering target, not universal driver or device compatibility.

Qualification requires verification of the exact GPU, firmware, kernel driver, Mesa version, and required graphics capabilities.

Graphics stack

The intended stack includes:

- Linux AMDGPU kernel driver.
- Mesa.
- RADV Vulkan driver.
- DRM/KMS interfaces.
- Wayland graphics integration.
- Photon compositor and color-management integration.

Graphics capability must be tested independently from basic device detection.

6. AMD XDNA NPU Support

The intended NPU scope includes:

- XDNA1.
- XDNA2.

The Linux "amdxdna" driver and associated userspace interfaces are part of the integration investigation.

NPU qualification must establish:

- Exact NPU identification.
- Driver availability and compatibility.
- Firmware requirements.
- Runtime initialization.
- Supported execution interfaces.
- Memory and synchronization behavior.
- Correctness under representative workloads.
- Resource and thermal behavior.

Advertised lane counts or theoretical compute capabilities must not be treated as measured application performance.

7. Hardware Discovery

OmniSilicon is responsible for AMD hardware discovery and capability reporting.

The intended hardware profile is:

/run/omni/hw-profile

The profile must distinguish:

- Detected hardware.
- Driver-bound hardware.
- Available capabilities.
- Validated capabilities.
- Unsupported or unavailable features.
- Qualification status.

Every capability must have a traceable detection and validation source.

No subsystem may assume that a capability exists merely because a processor or GPU belongs to a particular product family.

8. Firmware and Platform Dependencies

Hardware qualification must account for:

- BIOS and UEFI firmware.
- AGESA and platform firmware where applicable.
- CPU microcode.
- GPU firmware.
- NPU firmware.
- Memory configuration.
- PCIe configuration.
- IOMMU behavior.
- ACPI and power-management interfaces.
- Thermal and platform-controller behavior.

Firmware requirements must be documented for each qualified hardware configuration.

9. Qualification Levels

Level| Meaning
TARGETED| Included in the intended engineering scope
DETECTED| Hardware identification works
DRIVER-BOUND| Required driver successfully binds
FUNCTIONAL| Defined correctness tests pass
QUALIFIED| Required hardware and regression gates pass
PRODUCTION| Approved for a documented production release

A device must not skip qualification stages through assumption or marketing specifications.

10. Hardware Qualification Tests

Each hardware configuration should undergo applicable tests covering:

1. CPU identification and instruction safety.
2. Memory initialization and stability.
3. Kernel boot and device discovery.
4. GPU driver initialization.
5. Graphics rendering and Vulkan correctness.
6. NPU initialization and workload correctness.
7. IOMMU and DMA behavior.
8. Power management and thermal stability.
9. Suspend and resume behavior where supported.
10. Stress and regression testing.

Results must identify the exact hardware and software configuration.

11. Support Matrix Status

Hardware family| Intended scope| Current status
Phoenix| Zen 4 CPU| TARGETED
Hawk Point| Zen 4 CPU| TARGETED
Strix Point| Zen 5 CPU| TARGETED
Strix Halo| Zen 5 CPU| TARGETED
Gorgon Point| Zen 5 CPU| TARGETED
Gorgon Halo| Zen 5 CPU| TARGETED
gfx1100| Radeon GPU| TARGETED
gfx1103| Radeon GPU| TARGETED
gfx1150| Radeon GPU| TARGETED
gfx1151| Radeon GPU| TARGETED
gfx12xx| Radeon GPU| TARGETED
XDNA1| AMD NPU| TARGETED
XDNA2| AMD NPU| TARGETED

No hardware family in this table is represented as production-qualified.

12. Current Status

This document defines the intended AMD hardware support and qualification policy.

No completed hardware qualification, production driver validation, or measured accelerator performance is claimed.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — AMD-first engineering. Hardware support earned through evidence.