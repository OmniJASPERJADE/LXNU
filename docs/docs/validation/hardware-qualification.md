LXNU Hardware Qualification Policy

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architectures: AMD64 (Ryzen), ARM64 (Soundwave)
Status: Engineering specification
Execution status: NOT RUN

1. Purpose

This policy defines the process for evaluating, testing, and qualifying hardware for LXNU and its System-One integration.

It establishes the distinction between intended hardware support, hardware detection, driver availability, functional testing, qualification, and production support.

Listing a processor or device as a target does not establish that it works.

Qualification is performed per architecture. An AMD64 qualification result does not extend to ARM64. No ARM64 processor or platform is currently selected for qualification.

2. Qualification Principles

Hardware qualification must follow these principles:

- Qualify actual hardware, not assumed capabilities.
- Record exact hardware identifiers and revisions.
- Use pinned kernel and firmware versions.
- Validate driver binding and runtime operation.
- Test relevant failure and recovery conditions.
- Preserve test logs and reproducible evidence.
- Distinguish partial functionality from complete qualification.
- Requalify affected hardware after significant kernel, driver, firmware, or toolchain changes.

3. Hardware Scope

LXNU targets AMD64 and ARM64 systems using supported hardware.

The intended hardware scope includes:

3.1 AMD CPUs

Target families include:

- Zen 4.
- Zen 5.

Specific product families may include Phoenix, Hawk Point, Strix Point, Strix Halo, Gorgon Point, and Gorgon Halo.

Product-family inclusion is a target designation, not a qualification result.

3.2 AMD Radeon GPUs

Target GPU support includes applicable RDNA generations and AMDGPU integration.

Target GPU identifiers include:

- gfx1100.
- gfx1103.
- gfx1150.
- gfx1151.
- gfx12xx.

Each GPU must be identified and tested independently. A shared architecture designation does not guarantee identical functionality.

3.3 AMD XDNA NPUs

Target NPU support includes applicable XDNA1 and XDNA2 hardware through supported kernel drivers and userspace interfaces.

NPU detection alone does not establish usable acceleration.

4. Qualification Stages

Stage| Status meaning
Targeted| Hardware is within the intended design scope
Identified| Hardware identifiers are detected correctly
Driver-bound| The intended kernel driver binds to the device
Functional| Required device operations pass testing
Validated| Defined qualification tests pass
Qualified| All mandatory acceptance criteria are satisfied
Production-supported| Release and support requirements are approved

Stages must be recorded separately for each hardware configuration.

5. CPU Qualification

CPU qualification must verify:

- Correct vendor, family, model, and stepping identification.
- CPU topology and core enumeration.
- Multiprocessor initialization.
- Scheduler operation.
- Memory-management behavior.
- Power-management interfaces.
- Thermal monitoring and protection.
- Interrupt handling.
- Suspend and resume behavior where supported.
- Runtime ISA detection and safe dispatch.

Instruction-set validation

The baseline userspace target is x86-64-v3.

Higher instruction-set capabilities require runtime validation.

AVX-512 dispatch must verify applicable CPU feature bits and operating-system extended-state support, including the required XCR0 state.

No blanket "-march=znver5" assumption is permitted.

Safe fallback implementations must remain available.

6. GPU Qualification

GPU qualification must verify:

- PCI device identification.
- AMDGPU driver binding.
- Device initialization.
- DRM functionality.
- Memory allocation and management.
- Display and rendering paths.
- Vulkan and RADV compatibility where applicable.
- Compute workloads where supported.
- Suspend, resume, and reset behavior.
- Error reporting and recovery.

HDR qualification additionally requires a validated compositor-side color-managed rendering path and compatible display hardware.

GPU detection or successful driver loading alone does not establish graphics qualification.

7. NPU Qualification

NPU qualification must verify:

- Hardware identification.
- Driver availability and binding.
- Firmware compatibility.
- Userspace interface availability.
- Workload submission.
- Execution correctness.
- Resource and memory behavior.
- Error handling and recovery.
- Performance measurement where acceleration claims are made.

CPU fallback must remain available where required.

No NPU acceleration claim may be based solely on hardware presence or advertised lane count.

8. Platform Integration

Hardware must be tested as part of a complete platform configuration.

Relevant components include:

- CPU and memory.
- Firmware and UEFI configuration.
- PCIe topology.
- IOMMU.
- GPU and NPU devices.
- Storage controllers.
- Networking.
- Input devices.
- Power and thermal management.
- Kernel drivers and userspace services.

Individual component success does not establish whole-platform compatibility.

9. Test Environment Records

Each qualification report must identify:

1. Manufacturer and product model.
2. CPU family, model, and stepping.
3. GPU device ID and revision.
4. NPU identity where applicable.
5. System firmware version.
6. Memory configuration.
7. Kernel source revision.
8. Kernel configuration checksum.
9. Driver and firmware versions.
10. Compiler and toolchain versions.
11. Test procedures and results.
12. Logs and supporting evidence.

Test environments must be reproducible wherever practical.

10. Failure Classification

Qualification failures must be recorded as one of the following:

- Hardware detection failure.
- Driver initialization failure.
- Firmware incompatibility.
- Functional failure.
- Performance regression.
- Thermal or power-management failure.
- Security or isolation failure.
- Recovery failure.
- Insufficient test evidence.

Failures must not be concealed by changing the hardware support label.

11. Qualification Acceptance

A device may be marked qualified only when:

- Required identification tests pass.
- Required drivers operate correctly.
- Mandatory functional tests pass.
- Applicable security checks pass.
- Relevant failure and recovery tests pass.
- Known limitations are documented.
- Evidence is linked to the tested software and hardware revisions.
- The qualification record receives approval.

Production support requires additional release and maintenance commitments.

12. Requalification Triggers

Requalification may be required after changes to:

- Upstream Linux revisions.
- LXNU patches.
- Kernel configuration.
- AMDGPU or NPU drivers.
- Firmware.
- Compiler or linker toolchains.
- Hardware revisions.
- System-One integration contracts.

The affected qualification scope must be identified rather than assuming all prior results remain valid.

13. Current Hardware Status

The hardware families and device identifiers listed in this document are intended targets.

No CPU, GPU, NPU, or complete platform is declared qualified by this specification.

No successful hardware test, production driver qualification, or performance result is claimed.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Hardware support is demonstrated, not assumed.