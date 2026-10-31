LXNU Kernel Configuration Policy

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architectures: AMD64 (Ryzen), ARM64 (Soundwave)
Status: Engineering specification
Execution status: NOT RUN

1. Purpose

This policy defines how LXNU selects, maintains, reviews, and validates Linux kernel configuration options.

LXNU uses upstream Linux as its kernel foundation. Configuration changes must support the project's architecture and hardware requirements without unnecessarily duplicating upstream functionality.

2. Configuration Principles

All kernel configuration decisions must follow these principles:

- Prefer upstream Linux defaults when they meet project requirements.
- Enable only functionality justified by documented requirements.
- Disable unnecessary functionality only after compatibility and dependency review.
- Preserve required AMD platform support.
- Avoid unsafe architecture-wide instruction-set assumptions.
- Keep security, debugging, and diagnostic options deliberate.
- Make configuration changes reviewable and reproducible.
- Never treat a configuration choice as proof of runtime functionality.

3. Configuration Ownership

Configuration responsibilities are divided as follows:

Area| Responsibility
Upstream Linux| Core kernel functionality and hardware infrastructure
LXNU| Downstream configuration policy and justified integration changes
OmniSilicon| Hardware discovery and capability reporting
OmniRed| Workload classification and resource coordination
OmniSoft| Userspace integration
Omni Performance Libraries| Runtime-safe optimized operations

LXNU must not introduce competing implementations of upstream scheduler, memory-management, driver, or filesystem infrastructure without a documented architectural justification.

4. Architecture Baseline

LXNU maintains a separate kernel configuration for each production architecture.

AMD64

The baseline userspace architecture target is x86-64-v3.

Higher instruction-set capabilities must use runtime detection and safe dispatch.

In particular:

- Do not apply blanket "-march=znver5".
- Do not assume AVX-512 is available on every supported CPU.
- Validate CPU capabilities and operating-system extended-state support before using advanced instruction sets.
- Preserve safe fallback paths.

ARM64

The ARM64 configuration targets the platform baseline of the selected processor, not a
vendor-specific microarchitecture level.

Processor and SoC selection is not yet made. Configuration must not enable platform-specific
drivers or features for hardware that has not been selected and documented.

Architecture-specific options must be isolated in the amd64 and arm64 configuration files
rather than forced into a shared fragment.

Neither configuration may assume that every supported processor has the same optional
instruction-set capabilities.

5. Platform Hardware Support

AMD64 profile

The intended hardware scope includes:

CPUs

- AMD Ryzen Zen 4 family.
- AMD Ryzen Zen 5 family.

GPUs

- Supported AMD Radeon RDNA generations.
- AMDGPU driver integration.

NPUs

- AMD XDNA hardware through the appropriate upstream and platform interfaces.

These are target categories, not a declaration of completed hardware qualification.

Each configuration must be evaluated against the actual upstream kernel version and driver availability.

ARM64 profile

No processor, SoC, GPU, or NPU vendor has been selected for the Soundwave platform.

The ARM64 configuration must therefore enable only generic architecture support and the
drivers required by the selected platform once that selection is documented. It must not
pre-populate vendor drivers or adopt an assumed device tree/ACPI description.

Accelerator backends are independently qualified and are not inherited from the AMD64 profile.

6. Kernel Subsystems

Configuration review must account for:

- CPU architecture and platform initialization.
- SMP and CPU scheduling.
- Virtual memory and physical memory management.
- AMD IOMMU and device isolation.
- PCI and PCIe.
- AMDGPU and DRM.
- AMD power-management interfaces.
- Filesystem and block-device support.
- Networking.
- Input and device discovery.
- Tracing and diagnostics.
- Security and integrity facilities.

Subsystems must remain enabled or disabled according to documented platform requirements and dependency analysis.

7. Security Configuration

Security-related configuration must be reviewed as a coordinated system.

Areas include:

- Linux Security Module support.
- Landlock.
- Kernel lockdown.
- Yama.
- Integrity facilities.
- BPF security policy where justified.
- Module-signing capabilities.
- Kernel address-space and memory protections.

The intended System-One security direction includes Landlock, Lockdown, Yama, integrity, and BPF-related controls.

A configured security feature is not considered operational until its behavior has been tested.

8. Driver and Module Policy

Driver configuration must distinguish between:

- Built-in drivers.
- Loadable modules.
- Unsupported hardware.
- Experimental functionality.

Required boot-critical drivers must be available early enough to support the boot design.

Optional drivers should not be included without a documented compatibility or product requirement.

Module loading and trust policy must be documented before production deployment.

9. Debugging and Diagnostics

Development configurations may enable additional diagnostic facilities.

Production-oriented configurations must balance observability, security, binary size, and runtime overhead.

Debugging options must not be removed merely to improve reported performance.

Diagnostic capabilities and their overhead must be measured before making performance claims.

10. Configuration Change Management

Every downstream configuration change must include:

1. The affected kernel option.
2. The previous setting.
3. The proposed setting.
4. The technical justification.
5. Relevant upstream documentation or source reference.
6. Dependency and compatibility considerations.
7. Validation requirements.

Configuration changes must be reviewed alongside relevant kernel source and patch changes.

11. Configuration Validation

Before a configuration is accepted, applicable checks must include:

- Kernel configuration consistency.
- Dependency resolution.
- Required driver availability.
- Architecture compatibility.
- Security configuration review.
- Build validation.
- Boot validation.
- Hardware testing.
- Regression testing.

A successful configuration merge or build does not establish hardware qualification.

12. Reproducibility

Every qualified configuration must be traceable to:

- Exact upstream Linux revision.
- LXNU source revision.
- Configuration file and checksum.
- Toolchain versions.
- Build environment.
- Build logs.
- Generated artifact checksums.

Configuration changes must be version-controlled.

13. Current Status

This document defines the intended LXNU configuration policy.

No production kernel configuration, successful kernel build, boot validation, or hardware qualification is claimed by this document.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Configuration is an engineering decision, not a collection of unchecked options.
