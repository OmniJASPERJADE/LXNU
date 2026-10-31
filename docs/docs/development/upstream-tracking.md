LXNU Upstream Linux Tracking and Synchronization Policy

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Architecture: AMD64
Status: Engineering specification
Execution status: NOT RUN

1. Purpose

This document defines how LXNU tracks, evaluates, integrates, and maintains upstream Linux kernel source.

LXNU is a Linux-based kernel engineering project shaped by selected XNU-inspired architectural patterns. Upstream Linux remains the foundation for kernel functionality, hardware support, drivers, scheduling, memory management, networking, and filesystems.

LXNU must maintain a controlled relationship with upstream Linux rather than becoming an independently diverging kernel fork.

2. Upstream-First Principles

LXNU follows these principles:

- Upstream Linux is the authoritative kernel foundation.
- Prefer upstream functionality over downstream duplication.
- Track exact source revisions.
- Review upstream changes before integration.
- Maintain a small, documented downstream patch set.
- Preserve upstream licensing and attribution.
- Prioritize relevant upstream security fixes.
- Validate compatibility after synchronization.
- Never equate successful source synchronization with a validated kernel.

3. Upstream Source Authority

The primary upstream source is the official Linux kernel project:

- Repository: https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git
- Stable kernel releases: https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git

Official upstream repositories and their signed release or commit information should be used wherever available.

Mirrors may be used for retrieval reliability, but their contents must be verified against the authoritative source.

4. Kernel Version Strategy

The intended LXNU baseline targets Linux 6.18 LTS or newer, subject to project qualification.

Kernel selection must consider:

- Long-term support status.
- AMD CPU compatibility.
- AMDGPU and DRM development.
- AMD XDNA driver availability.
- Security fixes.
- Filesystem and storage compatibility.
- eBPF and LSM capabilities.
- Compiler and toolchain compatibility.
- System-One integration requirements.

A newer upstream kernel must not be adopted solely because its version number is higher.

The selected revision must be documented and justified.

5. Source Pinning

Every integration build must identify an exact upstream source revision.

Required metadata includes:

- Upstream repository.
- Kernel version.
- Git commit identifier.
- Release tag where applicable.
- Source archive checksum where applicable.
- Retrieval date.
- Signature verification result where available.

Moving branches such as "master" or "linux-6.18.y" must not serve as the immutable source identity for a qualified build.

A branch may identify the update channel, but the exact commit must identify the build input.

6. Update Monitoring

LXNU must monitor relevant upstream development in these areas:

- AMD64 architecture.
- AMD CPU and platform support.
- AMDGPU and DRM.
- XDNA and NPU-related drivers.
- Memory management.
- Scheduler and task management.
- Device discovery and driver infrastructure.
- IOMMU and DMA isolation.
- LSM and BPF security.
- Networking.
- Filesystems and block storage.
- Power and thermal management.
- Security advisories and stable fixes.

Monitoring does not authorize automatic integration.

Each relevant update requires impact assessment.

7. Update Classification

Upstream changes must be classified before integration.

Classification| Description
Security| Vulnerability fixes and security hardening
Critical bug fix| Fixes affecting system correctness or stability
Hardware enablement| New or improved AMD hardware support
Compatibility| Userspace, driver, or subsystem compatibility
Performance| Optimization requiring measurement
Maintenance| Refactoring and general maintenance
Experimental| Features requiring further evaluation

Security and critical correctness fixes receive priority review.

Experimental changes must not enter a qualified release without appropriate validation.

8. Synchronization Procedure

Each synchronization cycle must follow a documented process.

Stage 1 — Identify

Select the proposed upstream revision and record its exact commit.

Stage 2 — Review

Review relevant upstream changes, security fixes, subsystem modifications, and known regressions.

Stage 3 — Assess Downstream Impact

Identify affected LXNU patches, configuration options, interfaces, build scripts, and hardware requirements.

Stage 4 — Integrate

Retrieve the pinned source and apply the approved LXNU downstream patch series.

Stage 5 — Resolve Conflicts

Investigate patch conflicts individually.

Do not resolve conflicts through blind replacement or indiscriminate patch deletion.

Stage 6 — Validate

Run applicable source, configuration, build, static-analysis, and regression tests.

Runtime and hardware validation must follow where required.

Stage 7 — Record

Update the upstream revision record, patch inventory, configuration references, and validation evidence.

9. Downstream Patch Compatibility

Every downstream patch must be reviewed during synchronization.

For each patch, determine whether it is:

- Still required.
- Already available upstream.
- Superseded by a newer upstream implementation.
- Incompatible with the new revision.
- Ready for upstream submission.
- Suitable for retirement.

Patches that duplicate upstream functionality should be removed when safe and justified.

The patch inventory must reflect the actual integrated source tree.

10. Security Update Policy

LXNU must maintain a documented process for evaluating upstream security updates.

Security review must determine:

- Whether the vulnerability affects the selected revision.
- Whether LXNU carries related downstream changes.
- Whether a stable backport is available.
- Whether integration introduces regressions.
- Which validation tests are required.
- Whether release approval must be blocked.

A security fix must not be described as integrated until the source change and its validation evidence are recorded.

11. Fedora Integration Reference

Fedora Workstation is the primary upstream integration and compatibility reference for:

- Modern Linux kernel integration.
- eBPF and LSM-BPF.
- Mesa and RADV.
- LLVM and Clang.
- Creator and graphics tooling.

Fedora is a reference environment, not LXNU's kernel source authority or package-system foundation.

LXNU retains its independent architecture, repository, package policy, and release process.

12. Synchronization Records

Every synchronization cycle must record:

1. Previous upstream revision.
2. New upstream revision.
3. Reason for the update.
4. Relevant upstream changes.
5. Security impact.
6. Downstream patches affected.
7. Configuration changes.
8. Build and test results.
9. Known regressions.
10. Approval and integration status.

Records must be retained with the project's engineering documentation.

13. Rollback Policy

If synchronization introduces a critical regression, the project must be able to identify and restore the previous known source and configuration state.

Rollback records must identify:

- Previous upstream commit.
- Previous LXNU patch revision.
- Previous kernel configuration.
- Affected artifacts.
- Reason for rollback.
- Required follow-up work.

Rollback must not silently discard security fixes. Security implications must be reviewed before reverting an update.

14. Prohibited Practices

LXNU must not:

- Track an unpinned upstream branch as a qualified build source.
- Merge upstream changes without review.
- Remove upstream security fixes without documented justification.
- Carry unnecessary duplicate downstream functionality.
- Conceal unresolved synchronization conflicts.
- Claim compatibility without applicable tests.
- Claim hardware support based only on upstream driver presence.
- Describe proposed synchronization automation as operational before testing it.

15. Current Status

This document defines the intended LXNU upstream tracking and synchronization policy.

No completed upstream synchronization cycle, qualified kernel revision, maintained downstream patch series, or automated tracking process is claimed by this specification.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Stay aligned with upstream. Differentiate only where engineering demands it.