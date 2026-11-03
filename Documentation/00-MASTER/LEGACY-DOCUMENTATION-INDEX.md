# Legacy Documentation Index and Migration Map

The existing lower-case `docs/` tree contains LXNU-specific policies and validation specifications. It is preserved in place; this map connects those source documents to the canonical `Documentation/` structure without overwriting existing files or silently dropping content.

## Architecture and governance

| Preserved source | Canonical destination / relationship |
| --- | --- |
| `docs/architecture/overview.md` | `00-MASTER/ARCHITECTURE.md` and `01-LXNU/KERNEL-ARCHITECTURE.md` |
| `docs/architecture/component-boundaries.md` | `00-MASTER/ARCHITECTURE.md`; retain as detailed cross-component ownership source |
| `docs/architecture/architecture-profiles.md` | `01-LXNU/AMD64-PLATFORM.md`, `08-TOOLCHAIN/SIMD-ARCHITECTURE.md`, and `04-OMNISILICON/HARDWARE-QUALIFICATION.md` |
| `docs/manifesto.md` | Project context; link from `00-MASTER/SYSTEM-ONE-MASTER-SPEC.md` |
| `docs/vision/system-one-design-fiction.md` | Non-normative design fiction only; do not treat as engineering requirements |

## Kernel, platform, security, and interface policy

| Preserved source | Canonical destination / relationship |
| --- | --- |
| `docs/kernel/configuration-policy.md` | `01-LXNU/KERNEL-ARCHITECTURE.md` |
| `docs/docs/kernel/patch-policy.md` | `12-UPSTREAM/LINUX-UPSTREAM.md` and `01-LXNU/KERNEL-ARCHITECTURE.md` |
| `docs/docs/interfaces/abi-policy.md` | `02-OMNISOFT/RUNTIME-APIS.md` and `01-LXNU/KERNEL-ARCHITECTURE.md` |
| `docs/docs/security/kernel-security-policy.md` | `01-LXNU/SECURITY.md` |
| `docs/licensing.md` | `12-UPSTREAM/LINUX-UPSTREAM.md` and `08-TOOLCHAIN/BUILD-REPRODUCIBILITY.md` |
| `docs/platform/hardware-support.md` | `04-OMNISILICON/HARDWARE-QUALIFICATION.md` and `10-VALIDATION/HARDWARE-MATRIX.md` |

## Development and build policy

| Preserved source | Canonical destination / relationship |
| --- | --- |
| `docs/development/build-plan.md` | `08-TOOLCHAIN/COMPILER-ARCHITECTURE.md` and `08-TOOLCHAIN/CROSS-COMPILATION.md` |
| `docs/development/continuous-integration.md` | `10-VALIDATION/TEST-PLAN.md` and `10-VALIDATION/RELEASE-QUALIFICATION.md` |
| `docs/development/release-process.md` | `09-DISTRIBUTION/RELEASE-QUALIFICATION.md` (or `10-VALIDATION/RELEASE-QUALIFICATION.md` for release gates) |
| `docs/development/rust-policy.md` | `08-TOOLCHAIN/RUST-POLICY.md` |
| `docs/docs/development/dependency-management.md` | `08-TOOLCHAIN/BUILD-REPRODUCIBILITY.md` and `09-DISTRIBUTION/APK-PACKAGING.md` |
| `docs/docs/development/reproducible-builds.md` | `08-TOOLCHAIN/BUILD-REPRODUCIBILITY.md` |
| `docs/docs/development/upstream-tracking.md` | `12-UPSTREAM/LINUX-UPSTREAM.md` |

## Validation and audit

| Preserved source | Canonical destination / relationship |
| --- | --- |
| `docs/validation/gates.md` | `10-VALIDATION/RELEASE-QUALIFICATION.md` and `10-VALIDATION/TEST-PLAN.md` |
| `docs/docs/validation/test-strategy.md` | `10-VALIDATION/TEST-PLAN.md` |
| `docs/docs/validation/hardware-qualification.md` | `10-VALIDATION/HARDWARE-MATRIX.md` and `04-OMNISILICON/HARDWARE-QUALIFICATION.md` |
| `docs/audit/baseline-audit.md` | `10-VALIDATION/TEST-PLAN.md` as historical audit evidence; retain its audit date and scope |

## Status and safe migration rules

- The lower-case `docs/` sources remain intact and authoritative for their original LXNU-specific details until each is deliberately consolidated.
- Existing files in the numbered `Documentation/` tree are not overwritten by this mapping.
- Do not mark a legacy document as migrated until its substantive requirements, status labels, evidence, and references are carried over and reviewed.
- `docs/vision/system-one-design-fiction.md` is explicitly non-normative and must not be used as an engineering specification.
- Existing links may still point to `docs/`; update them only after the corresponding content is available at its canonical destination.
