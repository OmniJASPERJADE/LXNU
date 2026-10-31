LXNU Kernel Patch Management Policy

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architectures: AMD64 (Ryzen), ARM64 (Soundwave)
Status: Engineering specification
Execution status: NOT RUN

1. Purpose

This policy defines how LXNU manages downstream modifications to upstream Linux.

LXNU is built on upstream Linux and adopts selected XNU-inspired architectural patterns. It does not replace Linux with Mach, incorporate Mach source, or use Apple source code.

The objective is to maintain a small, traceable, technically justified downstream patch set.

2. Upstream-First Policy

Upstream Linux is the authoritative source for core kernel functionality.

LXNU must prefer:

1. Existing upstream functionality.
2. Existing upstream configuration options.
3. An upstream contribution where a required capability is missing.
4. A downstream patch only when upstream integration is not practical or sufficient.

A downstream patch must not duplicate an existing upstream subsystem without a documented architectural justification.

3. Patch Classification

Every downstream patch must be assigned a category.

Category| Description
Architecture| LXNU architecture and integration boundaries
AMD platform| AMD-specific integration or compatibility
ARM64 platform| ARM64-specific integration, firmware, or platform compatibility
Security| Security policy or justified security integration
Performance| Measured optimization with correctness safeguards
Compatibility| Required userspace or hardware compatibility
Diagnostics| Tracing, observability, and debugging
Revert| Removal of an earlier downstream change

Experimental patches must be clearly identified and must not be represented as production-ready.

4. Patch Requirements

Every patch must include:

- Unique identifier.
- Descriptive subject.
- Technical rationale.
- Affected subsystem.
- Applicable architectures (amd64, arm64, or both).
- Upstream source revision.
- Author and attribution information.
- License and copyright preservation.
- Dependencies on other patches.
- Applicable tests.
- Known limitations.

Patches must be small enough to review and maintain whenever practical.

Architecture-specific patches must be marked as such and must not change behavior on the
other architecture. Where a change is common to both, it belongs in a shared patch rather than
two divergent ones.

5. Upstream Linux Synchronization

LXNU must track an exact upstream Linux revision.

Updates must include:

1. Review of upstream changes.
2. Identification of affected LXNU patches.
3. Patch rebase or replacement.
4. Build and configuration checks.
5. Regression analysis.
6. Security-fix review.
7. Updated source provenance.

Upstream changes must not be merged blindly.

6. Patch Lifecycle

Proposal

A patch begins with a documented problem or requirement.

Review

Reviewers assess architecture, correctness, security, maintainability, licensing, and upstream alternatives.

Integration

Approved patches are applied to the pinned upstream source revision.

Validation

Applicable tests are executed and recorded.

Maintenance

Patches are periodically reviewed for upstream adoption, obsolescence, regressions, and compatibility.

Retirement

A patch must be removed when upstream functionality replaces it, its requirement disappears, or it is no longer maintainable.

7. Security Patch Handling

Security-related changes receive priority review.

The process must:

- Identify affected upstream versions.
- Determine whether LXNU carries related downstream modifications.
- Evaluate patch applicability.
- Preserve upstream security fixes.
- Record testing and remaining exposure.
- Avoid claiming remediation until verified.

Critical unresolved vulnerabilities block applicable release approval.

8. Performance Patch Requirements

Performance patches require evidence.

A performance patch must include:

- Defined workload.
- Baseline configuration.
- Modified configuration.
- Measurement methodology.
- Repeated results.
- Correctness testing.
- Hardware and software environment.
- Known trade-offs.

No speedup may be claimed solely because a patch enables an optimization or specialized instruction set.

Safe fallback behavior must be preserved where hardware capabilities vary.

9. Patch Rejection Conditions

A patch must be rejected or deferred when it:

- Duplicates upstream functionality without justification.
- Has unclear ownership or provenance.
- Violates licensing obligations.
- Introduces unsafe architecture assumptions.
- Lacks a test strategy.
- Creates an unnecessary maintenance burden.
- Makes unsupported security or performance claims.
- Conflicts with LXNU's documented architecture.

10. Patch Inventory

The project must maintain a patch inventory containing:

- Patch identifier.
- File or series location.
- Classification.
- Upstream status.
- Dependencies.
- Review status.
- Validation status.
- Retirement plan where applicable.

The inventory must reflect the actual patch set, not planned or hypothetical patches.

11. Source Organization

The preferred source structure separates:

- Pinned upstream Linux source.
- LXNU downstream patch series.
- Kernel configuration.
- Build metadata.
- Validation scripts and reports.
- Release documentation.

The project must preserve upstream copyright notices and SPDX identifiers.

It must not imply that the entire upstream Linux source is original LXNU code.

12. Current Status

This document defines the intended patch-management process.

No completed LXNU downstream patch series, successful patch rebase, or validated kernel integration is claimed.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Keep the foundation upstream. Make every downstream change earn its place.