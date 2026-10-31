LXNU Testing and Verification Strategy

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architectures: AMD64 (Ryzen), ARM64 (Soundwave)
Status: Engineering specification
Execution status: NOT RUN

1. Purpose

This document defines the testing and verification strategy for LXNU.

It establishes how engineering requirements are translated into tests, how results are recorded, and how evidence supports integration and release decisions.

Testing must distinguish between source-level correctness, successful compilation, runtime behavior, hardware compatibility, and production qualification.

Tests are executed and recorded per architecture. A result on AMD64 is not evidence for ARM64, and the reverse is equally true. Cross-compiled builds are tested on their target architecture, or in a target-architecture virtual machine where physical hardware is unavailable.

2. Verification Principles

LXNU verification follows these principles:

- Test requirements, not assumptions.
- Prefer repeatable and automated tests where practical.
- Preserve test logs and environment details.
- Separate test design from test execution.
- Record failures rather than silently excluding them.
- Do not treat compilation as proof of runtime correctness.
- Do not treat a successful boot as proof of hardware qualification.
- Do not claim performance improvements without controlled measurements.
- Re-run affected tests after relevant source, configuration, or toolchain changes.

3. Verification Levels

Level| Verification target| Example evidence
L0 — Review| Requirements and design| Review records
L1 — Static| Source and configuration| Static-analysis reports
L2 — Build| Compilation and linking| Build logs and artifact checksums
L3 — Component| Individual subsystem behavior| Unit and component tests
L4 — Integration| Interacting subsystems| Integration test reports
L5 — Runtime| Actual kernel execution| Runtime logs and test results
L6 — Hardware| Supported physical hardware| Hardware test records
L7 — Qualification| Release acceptance| Approved qualification report

Passing one level does not automatically satisfy the levels above it.

4. Test Categories

4.1 Source and Static Analysis

Evaluate:

- Source formatting and consistency.
- Compiler diagnostics.
- Static-analysis findings.
- Integer and memory-safety concerns.
- Concurrency and synchronization risks.
- Unsafe Rust usage where applicable.
- SPDX and licensing metadata.

Tools and rules must be documented and version-pinned where practical.

4.2 Build Verification

Verify:

- Source retrieval and revision pinning.
- Patch application.
- Configuration consistency.
- Compiler and linker compatibility.
- Successful compilation and linking.
- Artifact integrity.
- Reproducibility where required.

A successful build proves only that the tested source and configuration compiled in the recorded environment.

4.3 Component Testing

Test individual components and interfaces independently where practical.

Areas include:

- Kernel integration contracts.
- Memory-management behavior.
- Process and task behavior.
- Device discovery.
- AMD platform integration.
- Security interfaces.
- Userspace-facing interfaces.

4.4 Integration Testing

Verify interactions between:

- LXNU and upstream Linux subsystems.
- LXNU and OmniSilicon.
- LXNU and OmniRed.
- LXNU and OmniSoft.
- Kernel drivers and userspace services.
- Security controls and system services.

Integration testing must identify ownership and dependencies for each test.

4.5 Runtime and Boot Testing

Runtime testing must verify actual execution.

Applicable tests include:

- Boot completion.
- Kernel initialization.
- Device enumeration.
- Process creation and termination.
- Memory allocation and reclamation.
- Filesystem access.
- Networking.
- Module loading.
- Error handling.
- Recovery behavior.

Boot success must not be inferred from a successful build.

4.6 Hardware Testing

Hardware tests must record:

- CPU model and family.
- GPU model and driver.
- NPU model and driver, where applicable.
- Firmware versions.
- Kernel revision.
- Kernel configuration.
- Toolchain.
- Test environment.
- Results and known limitations.

Hardware targets remain unqualified until required tests pass on the relevant hardware.

4.7 Performance Testing

Performance measurements must specify:

- Workload and input data.
- Hardware configuration.
- Software and firmware versions.
- Baseline and modified builds.
- Measurement method.
- Warm-up and repetition policy.
- Variance and uncertainty.
- Power and thermal conditions where relevant.

Performance claims must be supported by repeatable evidence.

5. Architecture-Specific Verification

Testing must account for LXNU's AMD64 target and System-One integration.

CPU and ISA

- Confirm detected CPU capabilities.
- Validate operating-system extended-state support before advanced ISA dispatch.
- Verify safe fallback paths.
- Test supported processor families independently.
- Avoid assuming all AMD64 processors expose identical features.

GPU

- Verify AMDGPU driver binding.
- Confirm device initialization.
- Test relevant DRM and userspace integration.
- Record supported GPU generations and known limitations.

NPU

- Verify device discovery and driver availability.
- Test supported interfaces and workloads.
- Record actual capability reporting.
- Do not claim acceleration based solely on device detection.

6. Security Verification

Security testing must cover applicable:

- Privilege boundaries.
- Access-control behavior.
- Kernel attack surface.
- Memory-safety risks.
- Module trust.
- LSM and Landlock behavior.
- Lockdown and integrity controls.
- BPF policy behavior.
- Vulnerability and dependency review.

Security configuration must be tested in the running system before operational effectiveness is claimed.

7. Test Evidence

Every formal test record should contain:

1. Unique test identifier.
2. Requirement or gate reference.
3. Test objective.
4. Preconditions.
5. Test procedure.
6. Expected result.
7. Actual result.
8. Environment and hardware.
9. Source revision.
10. Logs and supporting artifacts.
11. Tester or automation identity.
12. Date and status.

Evidence must be traceable to the exact source and configuration tested.

8. Result Classification

Use these result states:

State| Meaning
NOT RUN| No execution evidence exists
PASS| Acceptance criteria satisfied
FAIL| Acceptance criteria not satisfied
BLOCKED| Test cannot proceed because of a dependency
INCOMPLETE| Execution occurred but evidence is insufficient
NOT APPLICABLE| Test does not apply, with documented justification

A test must not be marked PASS based on an expected or simulated result.

9. Regression Testing

Changes must trigger regression testing based on their affected components and dependencies.

At minimum, review whether a change affects:

- Existing kernel behavior.
- Upstream compatibility.
- Device drivers.
- Security boundaries.
- Userspace interfaces.
- Boot and recovery.
- Performance baselines.

Regression failures must be investigated and recorded.

10. CI Integration

Automated tests may be integrated into GitHub Actions or other documented CI infrastructure.

CI results must identify:

- Workflow and job.
- Source revision.
- Runner type.
- Toolchain.
- Test configuration.
- Exit status.
- Logs and artifacts.

Hosted CI must not be treated as a substitute for physical AMD hardware testing.

Self-hosted hardware runners require documented security and maintenance controls.

11. Release Acceptance

Release approval must reference the applicable validation gates defined in "docs/validation/gates.md".

Mandatory gates must pass or receive an explicitly documented exception approved by the designated project authority.

Exceptions must identify their scope, rationale, risk, and expiration or remediation plan.

No failed or unexecuted mandatory test may be represented as passed.

12. Current Verification Status

This document defines the intended testing and verification strategy.

It does not establish that tests, CI workflows, hardware laboratories, or qualification procedures are operational.

The current project status remains:

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Trust the evidence. Never substitute confidence for verification.