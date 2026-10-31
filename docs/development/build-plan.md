LXNU Build and Development Plan

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Target architectures: AMD64 (x86_64-linux-gnu), ARM64 (aarch64-linux-gnu)
Status: Build process specification
Execution status: NOT RUN

1. Purpose

This document defines how LXNU will acquire upstream Linux source, maintain downstream modifications, configure the kernel, and produce reproducible AMD64 build artifacts.

The objective is a traceable engineering process—not an undocumented collection of build commands.

A successful build is necessary but does not prove runtime correctness, hardware compatibility, security, or production readiness.

2. Upstream Kernel Foundation

LXNU uses upstream Linux as its kernel foundation.

The engineering target is Linux 6.18 LTS or a newer validated LTS release.

Before each development cycle, the project must:

1. Identify the exact upstream release.
2. Record the immutable Git commit.
3. Verify source provenance and integrity.
4. Record applicable upstream security fixes.
5. Review compatibility with required platform hardware.
6. Document the reason for selecting that revision.

A version number alone is insufficient to identify a reproducible source tree.

3. Source Organization

Keep upstream source and LXNU modifications separately identifiable.

Recommended repository organization:

LXNU/
├── LICENSE
├── README.md
├── SECURITY.md
├── CONTRIBUTING.md
├── docs/
│   ├── architecture/
│   ├── development/
│   ├── validation/
│   └── manifesto.md
├── kernel/
│   ├── config/
│   │   ├── amd64.config
│   │   └── arm64.config
│   ├── patches/
│   └── source.lock
├── scripts/
└── tests/

This is a proposed organization. Directories should be created as implementation requires them.

Do not commit a second complete copy of upstream Linux merely to represent LXNU.

4. Source Pinning and Patch Management

Every build must identify:

- Upstream Linux release.
- Exact upstream commit.
- Source retrieval method.
- Source integrity information.
- LXNU patch-set revision.
- Kernel configuration revision.
- Toolchain versions.
- Build environment.

Downstream patches must be individually reviewable and ordered.

Each patch should document its purpose, affected subsystem, upstream relationship, and validation requirements.

Prefer upstream submission when a change is generally useful and appropriate for Linux.

5. Toolchain Policy

The target compiler strategy is:

- Clang 21 or newer, subject to qualification.
- LLVM linker and supporting LLVM tools.
- Thin LTO where supported and validated.
- Pinned build-tool versions.
- Explicit configuration of required kernel build dependencies.
- Target triples: `x86_64-linux-gnu` and `aarch64-linux-gnu`.

The exact toolchain must be recorded for every build.

Each architecture has its own configuration, artifact namespace, and build log. Host and target
architecture are recorded separately for cross-compiled builds, and the cross toolchain is
pinned independently of the host toolchain.

A newer compiler is not automatically a better or compatible compiler.

Compiler upgrades require build, boot, correctness, and regression testing on each target
architecture independently. A cross-compilation success is not evidence of a successful boot.

6. CPU Optimization Policy

The production userspace baseline is x86-64-v3.

Kernel compilation must not assume that every supported CPU has the same advanced instruction set.

Do not apply blanket "-march=znver5" or other unsafe architecture-specific flags.

Advanced instruction dispatch must verify:

- Hardware CPU feature support.
- Operating-system extended-state support.
- Required XCR0 state.
- Correct fallback behavior.

The build must preserve compatibility with the declared hardware support matrix.

7. Kernel Configuration

Kernel configuration must be version-controlled and reviewed.

Configuration decisions must address:

- AMD CPU support.
- AMDGPU and required graphics interfaces.
- Supported XDNA hardware interfaces.
- Memory management.
- Filesystem and storage requirements.
- Networking.
- Security mechanisms.
- Debugging and diagnostic capabilities.
- Module and built-in driver policy.

Every enabled feature must have a documented purpose.

Experimental options must not silently become production requirements.

8. Build Procedure

Each architecture is built from its own configuration, into its own artifact directory, with
its own recorded metadata. A build for one target never reuses another target's artifacts as
evidence.

The intended development sequence is:

1. Select the target architecture (amd64 or arm64).
2. Retrieve the pinned upstream Linux source.
3. Verify source integrity.
4. Apply the reviewed LXNU patch set.
5. Load the version-controlled kernel configuration for that architecture.
6. Validate toolchain and build dependencies.
7. Compile for the selected target.
8. Preserve build logs and metadata.
9. Inspect generated artifacts.
10. Run static and configuration checks.
11. Proceed to boot and hardware testing only after the build passes.

The exact commands will be maintained in version-controlled build scripts after the environment has been qualified.

9. Reproducibility

Each build must record:

- Source commit.
- Patch-set revision.
- Configuration checksum.
- Compiler and linker versions.
- Build dependencies.
- Build environment.
- Build command and relevant environment variables.
- Artifact checksums.
- Build logs.

Reproducibility must be tested by independent rebuilds under controlled conditions.

A build that completes successfully is not automatically reproducible.

10. Build Artifacts

Generated artifacts should be separated from source files.

Artifacts must have traceable names and metadata identifying their source revision and configuration.

Do not publish an artifact as a production LXNU kernel until the required validation and release gates pass.

11. Continuous Integration

Future CI should validate:

- Source retrieval and integrity.
- Patch application.
- Configuration consistency.
- Compilation.
- Static checks.
- Reproducibility.
- Relevant regression tests.

CI success must not be presented as proof of successful hardware operation.

12. Failure Handling

Failed builds must retain useful logs and identify:

- The failing stage.
- Toolchain and source versions.
- Configuration.
- Relevant error output.
- Suspected cause.
- Corrective action.
- Retest result.

Do not conceal failed builds or overwrite evidence.

13. Current Status

This document specifies the intended build process.

No successful LXNU kernel build, reproducible artifact, bootable image, or qualified production toolchain is claimed.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Reproducible engineering. Verifiable results.