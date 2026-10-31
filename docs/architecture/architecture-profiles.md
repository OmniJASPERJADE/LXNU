LXNU Multi-Architecture Profiles

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architectures: AMD64 (Ryzen), ARM64 (Soundwave)
Status: Architecture specification
Execution status: NOT RUN

1. Purpose

This document is the canonical definition of the two production architecture profiles for
System-One and LXNU.

It exists so that architecture policy is stated once and referenced everywhere, rather than
restated with variations across build, configuration, release, and validation documents.

Both profiles are full production targets. ARM64 is not experimental, optional, or deferred.

No content in this document constitutes an implementation, a build, or a qualification result.

2. Production Profiles

AMD64 — Ryzen Platform

- CPU: AMD Ryzen, Zen 4 and Zen 5 families as defined in the hardware support matrix.
- Graphics: AMD Radeon RDNA where supported, through AMDGPU, Mesa/RADV, and DRM/KMS.
- Accelerators: AMD XDNA NPU where supported and validated.
- Userspace baseline: x86-64-v3.
- Optional path: x86-64-v4 after CPU feature detection and OS extended-state (XCR0) validation.
- Boot: Limine where supported by the platform firmware.

ARM64 — Soundwave Platform

- CPU: AArch64/ARM64 production target.
- Userspace baseline: the ARM64 architecture baseline defined by the selected platform, not a
  vendor-specific microarchitecture level.
- Graphics: independently qualified backend; no assumption that AMD RDNA hardware exists.
- Accelerators: independently qualified backend; no assumption that XDNA hardware exists.
- Boot: architecture-appropriate firmware and handoff (UEFI, device tree, or ACPI as selected),
  documented per platform rather than assumed identical to AMD64.
- Processor, SoC, GPU, and NPU vendors are NOT selected. No silicon specification may be
  invented to fill this gap.

PowerPC (including G3, G4, G5) is not a System-One production profile. It is outside the
current scope. Adding a third architecture is an architecture decision requiring explicit
authorization, a toolchain plan, and qualification gates; it must not be inferred from a
product reference.

3. Shared Architecture and Isolation

System-One maintains one platform architecture across both profiles:

- Architecture-independent components share source, interfaces, and behavior.
- Hardware-specific implementations are isolated behind documented interfaces.
- Architecture-specific code lives in dedicated files, directories, or backends; it does not
  leak into shared logic through conditional compilation without an interface boundary.
- Every capability is discovered at runtime; no profile may assume a feature because a
  processor family or product name implies it.
- Every optimized path has a portable fallback.
- Cross-component interfaces are architecture-neutral; architecture-specific data is carried
  as explicit capability records, not as implicit platform assumptions.

4. Capability Discovery Contract

OmniSilicon provides the capability model consumed by every other domain. For each capability
the model must distinguish:

1. Presence — hardware exists.
2. Capability — the hardware feature is architecturally available.
3. Driver availability — a kernel driver binds.
4. Runtime availability — the interface is usable in the running system.
5. Validated support — the complete software and hardware path passes its tests.

A capability is not advertised as available unless stage 5 has been reached for that exact
configuration. Discovery failure must report "unknown" or "unsupported", never "available".

5. ABI, Interfaces, and Packaging

- Userspace ABI: glibc on both profiles, unless an architecture-specific exception is approved
  and documented.
- Kernel/userspace ABI: documented per architecture; mechanisms that differ between AMD64 and
  ARM64 must be described separately rather than presented as one identical interface.
- Package architecture identifiers: "amd64" and "aarch64".
- Repositories are architecture-specific. A package must not be published for an architecture
  on which it has not been built and tested.
- Cross-component contracts are versioned and architecture-neutral; architecture-specific
  extensions require explicit review.
- No private implementation detail becomes a public interface without review.

6. Build and Toolchain

- Target triples: "x86_64-linux-gnu" and "aarch64-linux-gnu".
- Each profile has its own kernel configuration, package build, and artifact namespace.
- Host and target architectures are recorded separately for every cross-compiled build.
- Toolchains are pinned per profile; the compiler, linker, libc, and binutils versions are
  recorded in build metadata.
- A cross-compiled artifact is not evidence of a bootable system. Native builds and
  cross-compiled builds are validated independently.
- Blanket microarchitecture flags (for example "-march=znver5", "-mcpu=native") are prohibited
  in production builds; optimization is selected at runtime.
- Rust components declare an MSRV and supported target triples; production Rust uses pinned
  stable toolchains.
- Reproducible builds are required per architecture, with independent rebuild comparison.

7. Validation

- Gates G01–G14 in the validation specification apply to each architecture independently.
- A gate passes for one architecture only for that architecture; results are never pooled.
- Architecture-specific gates (firmware handoff, ISA feature dispatch, package/ABI checks,
  platform qualification) are defined in the validation specification.
- QEMU or equivalent virtualization may contribute evidence but does not replace physical
  hardware qualification.
- Every gate remains NOT RUN until evidence exists and is recorded.

8. Current Status

Both profiles are specified. Neither is implemented.

No kernel has been built for AMD64 or ARM64. No image has been booted on either architecture.
No hardware has been qualified. No performance or power measurement has been taken.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — One platform architecture. Two production targets. Evidence per architecture.
