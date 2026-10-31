LXNU Continuous Integration Specification

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architecture: AMD64
Status: CI architecture specification
Execution status: NOT RUN

1. Purpose

Continuous Integration (CI) will provide automated verification of LXNU source changes, kernel configurations, patch sets, build environments, and engineering requirements.

The objective is to detect defects early, maintain reproducibility, and prevent unvalidated changes from entering the release process.

CI success does not establish production readiness or hardware qualification.

2. CI Architecture

LXNU will use a staged validation model.

Stage A — Repository Integrity

Validate:

- Repository structure.
- Required documentation.
- SPDX identifiers and licensing metadata.
- Patch metadata and source provenance.
- Configuration file integrity.
- Formatting and whitespace.

Stage B — Static Validation

Validate:

- Kernel configuration consistency.
- Patch applicability.
- Source formatting.
- Static analysis where supported.
- Dependency and license metadata.
- Security-sensitive changes.

Stage C — Compilation

Validate:

- Pinned upstream Linux source retrieval.
- LXNU patch application.
- AMD64 kernel configuration.
- Clang and LLVM toolchain compatibility.
- Kernel compilation.
- Artifact metadata and checksums.

Stage D — Runtime Testing

Where suitable hardware or virtualized environments are available, validate:

- Kernel boot.
- Memory initialization.
- Process execution.
- Device discovery.
- Driver initialization.
- Basic networking.
- System stability.

Virtualized testing does not replace physical AMD hardware qualification.

Stage E — Hardware Qualification

Use dedicated AMD hardware runners to test applicable:

- Zen 4 and Zen 5 CPU configurations.
- Radeon GPU initialization and rendering.
- XDNA NPU initialization and execution.
- Power and thermal behavior.
- Suspend and resume.
- Hardware-specific regressions.

Hardware qualification remains a separate requirement from ordinary CI compilation.

3. GitHub Actions

GitHub Actions is the intended repository automation platform.

Workflow definitions will be stored under:

.github/workflows/

Proposed workflows:

Workflow| Responsibility
"repository.yml"| Repository integrity and documentation
"source.yml"| Upstream source and patch validation
"kernel-build.yml"| AMD64 kernel compilation
"static-analysis.yml"| Static checks and configuration review
"security.yml"| Dependency and security checks
"reproducibility.yml"| Controlled rebuild comparison
"hardware.yml"| Dedicated AMD hardware testing

These are proposed workflow names. No workflow is claimed to exist or run until its file is implemented and its execution is verified.

4. Runner Strategy

Hosted runners

Hosted runners may perform:

- Documentation validation.
- Source integrity checks.
- Patch checks.
- Configuration checks.
- Static analysis.
- Suitable compilation tasks.

The runner operating system and toolchain must be explicitly controlled.

Self-hosted AMD runners

Dedicated AMD64 hardware is required for meaningful physical hardware qualification.

Self-hosted runners should identify:

- CPU model and family.
- GPU model and architecture.
- NPU availability.
- Firmware versions.
- Kernel version.
- Toolchain versions.
- Memory configuration.

Runners must be isolated from untrusted pull-request code.

Do not expose signing keys, deployment credentials, or other secrets to untrusted workflows.

5. Toolchain and Build Control

The target compiler strategy is Clang 21 or newer, subject to qualification.

Build environments must pin:

- Upstream Linux commit.
- LXNU patch revision.
- Kernel configuration.
- Compiler and linker.
- Build dependencies.
- Relevant environment variables.

Thin LTO may be used where supported and validated.

Toolchain changes require documented compatibility and regression testing.

6. Build Artifacts

CI artifacts should include:

- Kernel image.
- Relevant modules.
- Build logs.
- Configuration.
- Source revision.
- Patch-set revision.
- Compiler and linker versions.
- Artifact checksums.

Artifacts must be traceable to the exact source and configuration that produced them.

Unvalidated artifacts must not be presented as production releases.

7. Reproducible Builds

Reproducibility testing must compare independent builds using controlled inputs.

The process must identify:

- Source revision.
- Build configuration.
- Toolchain.
- Build environment.
- Generated artifact checksums.
- Differences between independent builds.

Known nondeterministic inputs must be documented and investigated.

A successful compilation alone does not establish reproducibility.

8. Security Controls

CI must follow least-privilege principles.

Required practices include:

- Minimal workflow permissions.
- Protected release branches.
- Review requirements for sensitive changes.
- Dependency vulnerability checks.
- Secret isolation.
- Pinned third-party workflow dependencies where practical.
- Artifact provenance.
- Auditability of release operations.

Untrusted pull requests must not receive privileged deployment or signing credentials.

9. Failure Policy

A failed mandatory workflow blocks the affected change from being treated as validated.

Every failure should preserve:

- Workflow name.
- Commit identifier.
- Runner environment.
- Toolchain versions.
- Relevant logs.
- Failure stage.
- Corrective action.
- Retest result.

Do not suppress failures merely to obtain a green workflow status.

10. Branch and Release Protection

The intended repository policy includes:

- Pull-request review for significant changes.
- Required CI checks before protected-branch merges.
- Restricted release permissions.
- Review of kernel and security-sensitive changes.
- Tagged source revisions for releases.
- Retained build evidence.

These controls must be configured in GitHub before they can be considered active.

11. CI and Validation Gate Relationship

CI provides evidence for the validation gates defined in "docs/validation/gates.md".

CI does not automatically pass a gate merely because a workflow succeeds.

For example:

- Compilation can contribute evidence to G05.
- Boot testing can contribute evidence to G06.
- Hardware runners can contribute evidence to G08 and G09.
- Controlled benchmarks can contribute evidence to G12.
- Regression workflows can contribute evidence to G13.

Final gate status requires review of the complete acceptance criteria and supporting evidence.

12. Current Status

This document defines the intended CI architecture.

No GitHub Actions workflow, self-hosted AMD runner, automated kernel build, reproducibility test, or hardware qualification pipeline is claimed to be operational.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Automate the checks. Preserve the evidence. Earn the release.