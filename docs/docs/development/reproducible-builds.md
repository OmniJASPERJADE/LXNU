LXNU Reproducible Build and Artifact Integrity Policy

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architectures: AMD64 (Ryzen), ARM64 (Soundwave)
Status: Engineering specification
Execution status: NOT RUN

1. Purpose

This document defines the requirements for reproducible LXNU builds, source provenance, artifact integrity, and build-environment traceability.

The objective is to ensure that published artifacts can be traced to their source inputs and that independent builds can be compared using documented procedures.

A successful compilation does not automatically establish reproducibility or artifact integrity.

Reproducibility is evaluated independently per architecture and per target triple. Rebuild comparison evidence is recorded separately for amd64 and aarch64 artifacts.

2. Core Principles

LXNU build engineering must follow these principles:

- Pin all significant source dependencies.
- Record exact upstream Linux revisions.
- Track all LXNU downstream patches.
- Pin production toolchains.
- Control build inputs and environment variables.
- Avoid undeclared network dependencies during compilation.
- Record build configuration and generated artifacts.
- Verify artifact checksums.
- Preserve build logs and provenance records.
- Investigate unexplained differences between builds.

Reproducibility must be demonstrated through independent comparison, not assumed from build configuration.

3. Source Provenance

Every build must identify its complete source inputs.

Required records include:

- Upstream Linux repository and commit.
- LXNU repository revision.
- Downstream patch-series revision.
- Kernel configuration revision and checksum.
- Build scripts and metadata.
- External dependency versions.
- Firmware and microcode references where applicable.
- License and copyright information.

Source inputs must be retrieved from documented and trusted locations.

Moving branches and unpinned dependency references must not be treated as immutable build inputs.

4. Toolchain Policy

Production builds must use documented and pinned toolchains.

The intended toolchain direction includes:

- Clang 21 or newer, subject to qualification.
- LLVM and LLD components with recorded versions.
- Stable Rust for production Rust components.
- Pinned Rust toolchains.
- Explicit minimum supported Rust version (MSRV).
- Documented assembler, linker, and utility versions.

Toolchain updates require compatibility review and applicable regression testing.

A newer compiler must not be assumed to produce equivalent or better results without validation.

5. Build Environment

The build environment must document:

- Operating system and version.
- Build host architecture.
- CPU and relevant hardware characteristics.
- Compiler and linker versions.
- Build dependencies.
- Environment variables.
- Build flags.
- Locale and timezone where relevant.
- Filesystem and relevant build-path settings.
- Network access policy.
- Build scripts and invocation parameters.

Undocumented host-specific dependencies must be identified and eliminated where practical.

6. Deterministic Build Requirements

The build process should control sources of nondeterminism, including:

- Timestamps.
- Filesystem traversal order.
- Archive member ordering.
- Unstable generated identifiers.
- Locale-dependent output.
- Uncontrolled environment variables.
- Randomized build inputs.
- Absolute build paths.
- Unpinned dependencies.

Where supported, reproducible-build techniques such as "SOURCE_DATE_EPOCH" should be used.

Any unavoidable nondeterministic output must be documented and excluded from byte-for-byte comparison only with a technical justification.

7. Build Isolation and Dependencies

Build dependencies must be declared and traceable.

The build system should:

- Separate build-time and runtime dependencies.
- Avoid downloading undeclared dependencies during compilation.
- Use verified source archives or pinned repository revisions.
- Validate dependency checksums.
- Review dependency licenses.
- Audit relevant dependency vulnerabilities.
- Prevent untrusted build inputs from silently entering the artifact.

Build isolation requirements must be proportional to the security and reproducibility risks.

8. Independent Rebuild Verification

A reproducibility test must compare outputs from independent builds using equivalent declared inputs.

The process must:

1. Retrieve the same pinned source revision.
2. Apply the same documented patch series.
3. Use equivalent toolchains and build configurations.
4. Build in separate environments.
5. Compare generated artifacts.
6. Identify and investigate differences.
7. Preserve logs and comparison results.

A reproducibility claim requires recorded evidence.

9. Artifact Integrity

Every release artifact must have a corresponding integrity record.

Applicable artifacts include:

- Kernel images.
- Kernel modules.
- Debug symbols.
- Build metadata.
- Source archives.
- Configuration files.
- Release packages.

Integrity records should include:

- Artifact filename.
- Artifact type.
- Source revision.
- Build identifier.
- Build configuration.
- Artifact size.
- SHA-256 checksum or stronger approved digest.
- Build timestamp or controlled source epoch.
- Provenance metadata.

Checksums establish whether an artifact matches a recorded digest. They do not independently prove that the artifact is trustworthy.

10. Signing and Trust

Artifact signing must be introduced with a documented key-management process.

That process must define:

- Signing authority.
- Key generation and protection.
- Authorized signing identities.
- Verification procedures.
- Key rotation.
- Revocation.
- Recovery procedures.
- Separation between build and signing privileges.

Signing must not be claimed operational until the signing infrastructure and verification process have been implemented and tested.

11. Build Attestation

Where practical, build records should capture machine-readable provenance.

Attestation records should identify:

- Source materials.
- Build dependencies.
- Toolchain.
- Build configuration.
- Build environment.
- Build process.
- Output artifact digests.

Attestation is supporting evidence, not a substitute for independent verification.

12. Failure Handling

Build and reproducibility failures must be recorded.

Examples include:

- Source retrieval failure.
- Dependency mismatch.
- Patch application failure.
- Compiler or linker failure.
- Configuration mismatch.
- Artifact checksum mismatch.
- Independent rebuild mismatch.
- Missing provenance information.

Unexplained artifact differences block a reproducibility claim and may block release approval.

13. CI Integration

CI workflows may automate:

- Pinned source retrieval.
- Dependency verification.
- Build execution.
- Artifact checksums.
- Provenance generation.
- Independent rebuild comparisons.
- Build-log retention.

CI infrastructure must identify the exact workflow, runner, source revision, toolchain, and result.

The existence of a proposed CI design does not establish that automated builds or reproducibility checks are running.

14. Release Requirements

Before an artifact is approved for release, applicable requirements include:

- Verified source provenance.
- Recorded toolchain and configuration.
- Successful build evidence.
- Artifact integrity records.
- License and dependency review.
- Security review.
- Reproducibility evidence where required.
- Release approval.

Exceptions must be documented and approved. They must not be presented as successful reproducibility verification.

15. Current Status

This document defines the intended LXNU reproducible-build and artifact-integrity policy.

No reproducible LXNU kernel build, independent rebuild comparison, signing infrastructure, or production artifact attestation is claimed.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Every artifact must have a traceable origin. Every claim must have evidence.