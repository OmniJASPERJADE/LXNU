Dependency Management and Supply Chain Policy

Project: LXNU / System-One
Status: Specification only — NOT RUN
Applies to: Kernel, C, C++, Rust, LLVM, build tooling, and supporting dependencies

1. Purpose

This policy defines how LXNU and System-One evaluate, approve, pin, audit, update, and verify software dependencies.

The objectives are to:

- Minimize unnecessary dependencies and reduce attack surface.
- Preserve reproducible and traceable builds.
- Prevent unreviewed dependency changes from entering production.
- Maintain license compliance and source provenance.
- Track known vulnerabilities and security advisories.
- Keep upstream Linux and the System-One integration layer maintainable.

A dependency being available upstream, included in a distribution, or enabled in a build does not automatically make it approved.

2. Scope

This policy applies to:

- Linux kernel source and selected upstream patches.
- C and C++ libraries and build dependencies.
- Stable Rust toolchains, crates, and build tooling.
- LLVM, Clang, LLD, compiler runtimes, and related utilities.
- Kernel configuration, firmware, generated code, and build-time tools.
- Documentation, testing, validation, packaging, and release tooling.
- Dependencies used by OmniSoft, OmniRed, OmniSilicon, Photon, and other System-One components where applicable.

Runtime dependencies and build-only dependencies must be tracked separately.

3. Dependency approval

Every proposed dependency must have a documented technical justification.

Review must consider:

1. Required functionality and whether an existing approved component can provide it.
2. Project activity, maintenance status, and upstream governance.
3. Security history and vulnerability response practices.
4. License compatibility and redistribution obligations.
5. Supported architectures and compatibility with the AMD64 target.
6. Build reproducibility and source availability.
7. Runtime overhead, binary size, and maintenance burden.
8. Whether the dependency introduces unnecessary services, privilege, or attack surface.

Dependencies should not be added solely for convenience when a smaller, maintainable alternative is practical.

Approval must identify the owning component and responsible maintainers.

4. Version pinning and updates

Production builds must use explicit dependency versions or immutable source revisions.

The project must not rely on unbounded version ranges, floating Git branches, or unverified latest-version resolution for release artifacts.

Each approved dependency record should include:

- Project and component name.
- Exact version or immutable source revision.
- Upstream source location.
- Owning System-One component.
- License identifier.
- Source checksum or equivalent integrity reference.
- Required build options and patches.
- Approval and review status.

Updates require review of upstream changes, compatibility, security impact, license changes, and reproducibility.

Security updates may receive expedited review, but must retain source verification and documented validation.

5. Source provenance and integrity

All dependencies must have traceable origins.

The project must prefer:

- Official upstream source repositories.
- Signed upstream release artifacts when available.
- Verified source archives and cryptographic checksums.
- Immutable commits or release tags backed by verified source.
- Documented patches with clear origin and purpose.

Downloaded source must not be treated as trustworthy merely because it came from a familiar mirror or package repository.

Unverifiable, modified, or unexplained source artifacts must be rejected pending investigation.

Generated source and vendored dependencies must retain enough provenance information to identify their original source and generation process.

6. License review

Every dependency must receive a license review before approval.

Review must establish:

- The applicable license and version.
- Copyright and attribution requirements.
- Source redistribution and modification obligations.
- Binary redistribution obligations.
- Notice and documentation requirements.
- Compatibility with the intended distribution model.
- Whether static linking, dynamic linking, or incorporation changes the applicable obligations.

SPDX identifiers should be used where applicable.

The project must preserve upstream copyright and licensing notices. No dependency may be assumed to be GPL-compatible, permissively licensed, or unrestricted without review.

The existing repository-level GPL-2.0 license must not be interpreted as automatically relicensing third-party source or every future component.

License uncertainty blocks production approval until resolved.

7. Security and vulnerability management

Dependencies must be monitored for known vulnerabilities and relevant security advisories.

Security review should include:

- Upstream security announcements.
- CVE records and applicable vulnerability databases.
- Maintainer advisories and release notes.
- Known exploited vulnerability information where relevant.
- Dependency-specific security notices.
- Vulnerability reports from project testing and review.

Findings must be assessed for actual exposure, affected versions, reachable code, configuration, and available mitigations.

A vulnerability scanner reporting no findings does not prove that a dependency is secure.

High-risk or actively exploited vulnerabilities require prompt triage. The project must document the affected component, severity assessment, mitigation or update decision, and validation evidence.

Unmaintained dependencies with unresolved critical security exposure must not be approved for production use.

8. C and C++ dependencies

C and C++ dependencies must use supported, explicitly selected versions.

Review must address:

- Compiler and standard-library compatibility.
- ABI and symbol compatibility.
- Memory safety and input validation.
- Undefined behavior and concurrency risks.
- Build-system behavior and generated code.
- Architecture-specific optimizations and safe fallbacks.
- License and transitive dependency obligations.

Compiler optimization must not introduce an unsafe baseline. Runtime-specific instruction dispatch requires verified CPU capability detection and a correct fallback path.

Third-party libraries must not silently replace core Linux kernel functionality or create competing ownership of kernel subsystems.

9. Rust dependencies

Production Rust code must use stable Rust.

The project must define and pin its production toolchain and explicit Minimum Supported Rust Version (MSRV) for each applicable component.

Rust dependency review must include:

- "Cargo.toml" and "Cargo.lock" review.
- Transitive dependency inspection.
- License and provenance checks.
- Vulnerability and maintenance review.
- Feature selection and unnecessary dependency removal.
- Unsafe-code inspection.
- Reproducible build considerations.

Production builds must not depend on unreviewed Git branches or uncontrolled dependency resolution.

"unsafe" Rust requires a documented safety justification and review of its invariants, ownership assumptions, aliasing, memory validity, and concurrency behavior.

Rust complements C and C++; it does not mandate wholesale replacement of existing kernel or systems code.

10. LLVM and toolchain dependencies

LLVM, Clang, LLD, compiler runtimes, and related tooling are part of the trusted build environment.

Their versions must be explicitly selected and recorded.

Toolchain changes require evaluation of:

- Linux kernel build compatibility.
- C, C++, and Rust interoperability.
- Linker behavior and generated artifacts.
- Debug information and symbol handling.
- LTO behavior.
- Architecture-specific code generation.
- Reproducibility and build performance.
- Security advisories and upstream maintenance.

The targeted LLVM/Clang version is not evidence that the toolchain has been successfully integrated or qualified.

11. Transitive and vendored dependencies

Direct dependencies must not be reviewed in isolation.

The project must identify and review transitive dependencies where technically possible.

Vendoring requires:

- A documented reason.
- Exact upstream source identification.
- License and security review.
- A documented update procedure.
- Clear separation between upstream source and local modifications.

Vendoring must not be used to hide untracked forks, bypass review, or avoid dependency maintenance.

12. Build isolation and reproducibility

Dependency retrieval and build execution must be controlled and traceable.

Build environments should:

- Use pinned toolchains and dependency revisions.
- Separate source retrieval from compilation.
- Avoid uncontrolled network access during compilation.
- Record build configuration and environment inputs.
- Preserve source checksums and build logs.
- Support independent rebuild verification.

Build-time tools must not automatically become runtime dependencies.

Dependency updates must be reflected in the appropriate lockfiles, source manifests, build definitions, and provenance records.

13. Dependency inventory

The project should maintain a machine-readable dependency inventory for approved production and build dependencies.

The inventory should record:

- Component and dependency identifiers.
- Exact versions and source revisions.
- Direct or transitive status.
- Build-time or runtime classification.
- License and copyright information.
- Source provenance and integrity references.
- Security review status.
- Owning component.
- Approval and update history.

A Software Bill of Materials (SBOM) should be generated for release candidates when the build infrastructure supports reliable generation and verification.

An SBOM is an inventory, not proof of security or license compliance.

14. Exceptions

Exceptions require documented justification, an identified owner, scope, risk assessment, mitigation, and review date.

Exceptions must not silently become permanent policy.

A dependency with unresolved provenance, licensing, or critical security concerns must not be promoted into a production release merely because an exception is convenient.

15. Validation requirements

Before production approval, the project must be able to demonstrate:

- Dependency versions and source revisions are pinned.
- Source provenance and integrity are recorded.
- License review is complete.
- Relevant security advisories have been assessed.
- Transitive dependencies have been considered.
- Build inputs are documented.
- Required tests and compatibility checks have passed.
- Exceptions are recorded and approved.

Validation results must distinguish:

- PASS — required evidence satisfies the gate.
- FAIL — a requirement is not satisfied.
- BLOCKED — validation cannot proceed.
- NOT RUN — no qualifying validation evidence exists.

No dependency is considered production-qualified solely because it appears in a manifest or builds successfully once.

16. Current project status

This document defines intended policy only.

- Dependency inventory: NOT RUN.
- Complete license audit: NOT RUN.
- Vulnerability audit: NOT RUN.
- Transitive dependency audit: NOT RUN.
- SBOM generation: NOT RUN.
- Reproducibility verification: NOT RUN.
- Production dependency approval: NOT CLAIMED.

Specified. NOT RUN. No gate measured. No component claimed to ship.