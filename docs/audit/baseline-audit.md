# LXNU — Baseline Repository Audit

**Repository:** `OmniJASPERJADE/LXNU`
**Branch:** `main`
**Revision audited:** `c05cfdb` (2026-10-31)
**Audit date:** 2026-10-31
**Scope:** repository content, structure, documentation, build readiness
**Method:** static inspection only — `git`, `find`, `grep`, `sha256sum`, GitHub API
**Result:** **no implementation exists; every validation gate remains NOT RUN**

This audit records what is present and what is absent. It does not build, modify, or validate anything.
No kernel was compiled. No image was booted. No hardware was tested.

---

## 1. Executive summary

The repository is a documentation set. It contains 23 files, 4,640 lines of Markdown, and
**zero source, build, or CI files**. The architecture, policies, and gate definitions are
internally consistent and unusually disciplined about not claiming results. The engineering
work they describe has not started.

The single most important finding is structural: a platform-wide document
(`docs/architecture/component-boundaries.md`) that assigns ownership across six domains lives
inside a repository that owns only one of them, and the other five have no repository at all.

---

## 2. Inventory

Commands: `find . -type f`, `wc -l`, `sha256sum`.

| Metric | Value |
|---|---|
| Tracked files | 23 |
| Markdown files | 21 |
| Markdown lines | 4,640 |
| Source files (`.c`, `.h`, `.S`, `.rs`) | 0 |
| Build files (`Makefile`, `Kconfig`, `APKBUILD`, `Cargo.toml`, `meson.build`) | 0 |
| CI workflows (`.github/workflows/*`) | 0 |
| Kernel config / `source.lock` / patches | 0 |
| Git commits | 6 |
| Branches | `main` only |
| Tags / releases | 0 |
| License | GPL-2.0 (verbatim `LICENSE`, no SPDX headers) |

Files:

```
CONTRIBUTING.md                                   4,840 B
LICENSE                                          18,092 B
README.md                                         4,906 B
SECURITY.md                                       4,119 B
docs/architecture/component-boundaries.md        16,627 B
docs/architecture/overview.md                     5,910 B   <- filename ends with a space
docs/development/build-plan.md                    6,113 B
docs/development/continuous-integration.md        6,906 B
docs/development/release-process.md               5,416 B
docs/development/rust-policy.md                  12,502 B
docs/kernel/configuration-policy.md               6,259 B
docs/licensing.md                                 4,704 B
docs/manifesto.md                                 2,408 B
docs/platform/hardware-support.md                 6,434 B
docs/validation/gates.md                          6,225 B
docs/docs/development/dependency-management.md   11,411 B
docs/docs/development/reproducible-builds.md      7,805 B
docs/docs/development/upstream-tracking.md        8,435 B
docs/docs/interfaces/abi-policy.md                6,698 B
docs/docs/kernel/patch-policy.md                  5,409 B
docs/docs/security/kernel-security-policy.md      7,715 B
docs/docs/validation/hardware-qualification.md   7,084 B
docs/docs/validation/test-strategy.md             8,042 B
```

---

## 3. Domain mapping

| Domain | Directory in repo | Source files | Documentation | State |
|---|---|---|---|---|
| LXNU | — (docs only) | 0 | architecture, kernel config, patch, ABI, security, validation | spec only |
| OmniSoft | none | 0 | none | absent |
| OmniRed | none | 0 | none | absent |
| OmniSilicon | none | 0 | `docs/platform/hardware-support.md` (policy prose) | absent |
| Omni Performance Libraries | none | 0 | dispatch policy inside architecture doc | absent |
| System-One OS | none | 0 | platform-wide boundaries doc | absent |

No repository on the `OmniJASPERJADE` account covers OmniSoft, OmniRed, OmniSilicon, the
performance libraries, or System-One OS integration. Public repositories at audit time:
`LXNU`, `pear-calamares-config`, `BareMetal`.

---

## 4. Findings

Severity: **Critical** blocks all progress; **High** blocks a milestone; **Medium** causes
drift or broken navigation; **Low** cosmetic/process.

### F-01 — No implementation of any kind (Critical)

Zero `.c`, `.h`, `.S`, `.rs` files; no `kernel/`, `scripts/`, `tests/` directories. The
`build-plan.md` §3 "Source Organization" describes these directories as proposed, and they do
not exist.

Impact: G01–G14 cannot be started. Nothing in the project has ever been built.

### F-02 — No pinned inputs or build system (High)

- No `kernel/source.lock`, no upstream commit pin, no patch queue.
- No kernel configuration file, although `configuration-policy.md` requires one to be version-controlled.
- No build script; `build-plan.md` §8 defers "exact commands" to a future qualified environment.
- No `APKBUILD`, `Makefile`, `Cargo.toml`, or toolchain lock.

Impact: build reproducibility (G02) is undefined, not merely unrun.

### F-03 — No CI despite a CI specification (High)

`continuous-integration.md` defines Stages A–D and proposed workflows under
`.github/workflows/`, then states at line ~254 that no workflow exists. Confirmed: the
directory is absent. Stage A ("Repository Integrity") would not even pass today, because of
F-05 and F-06.

### F-04 — Platform-wide ownership document inside a single-domain repository (High)

`component-boundaries.md` assigns responsibilities for six domains, but:

- it lives in the LXNU repository, which owns only the kernel domain;
- the other five domains have no repository;
- there is no System-One meta-repository to own cross-domain contracts.

This contradicts the document's own §13 change-management rule: an unreviewed repository
layout silently transfers architectural ownership. Either the document moves to a platform
repository, or the repository is renamed and re-scoped.

### F-05 — Broken internal references (Medium)

`docs/architecture/overview.md` has a trailing space in its filename. Referencing it as
`docs/architecture/overview.md` fails on GitHub and in any filesystem:

- `README.md:84`
- `CONTRIBUTING.md:14`

Both links are dead as written.

### F-06 — Nine documents misplaced under `docs/docs/` (Medium)

Affected: `dependency-management`, `reproducible-builds`, `upstream-tracking`, `abi-policy`,
`patch-policy`, `kernel-security-policy`, `hardware-qualification`, `test-strategy`.

Expected locations are `docs/development/`, `docs/interfaces/`, `docs/kernel/`,
`docs/security/`, `docs/validation/`. These are not duplicates of existing files — they are
documents that landed one level too deep, so no top-level index reaches them. Likely an
upload path error, same class of defect as the corrupted filename fixed in `c05cfdb`.

### F-07 — Undefined components referenced as if they exist (Medium)

`OrbionFS`, `Photon`, `OmniWorks`, `Omni Graph`, `Symphony`, `Director's Cut`,
`System-One Health` are named in the architecture without definition, repository, interface,
or owner assignment beyond a sentence. `OrbionFS` appears in `README.md` and the boundaries
document but nowhere in `docs/` as a specification. Any reader will assume these exist.

### F-08 — README formatting and heading inconsistency (Low)

- `README.md:48–55` renders a malformed table (`Component| Responsibility` without pipes or
  a separator row).
- Most documents use plain-text headings (`1. Purpose`) instead of Markdown `#`, so GitHub
  shows no outline and no anchored TOC. `README.md` alone uses real Markdown headings.

### F-09 — Version identity is prose only (Low)

`1.6.6.2ɓ` appears 21 times, consistently. It is not bound to a tag, a commit, or an artifact
manifest, so it cannot identify a build. G01/G02 require exactly that binding.

### F-10 — License metadata incomplete (Low)

`LICENSE` is GPL-2.0 verbatim. No SPDX identifiers in any file, no per-directory licensing,
no statement on how GPL-2.0-only kernel code combines with planned userspace components.
`licensing.md` discusses provenance but the repository itself carries no machine-readable
license metadata.

### F-11 — No security reporting channel (Low)

`SECURITY.md` uses GitHub private vulnerability reporting **if enabled**, with a fallback to
"an appropriate private channel". No address, no PGP key, no advisory link. Unverifiable from
the repository whether the feature is enabled.

### F-12 — No review or protection metadata (Low)

Six commits, all direct to `main`, all on 2026-10-31. No `CODEOWNERS`, no PR template, no
branch-protection evidence, no signed commits. The change-management policy in §13 is
therefore unenforced by tooling.

### F-13 — Gate register cannot be executed as written (Info)

`gates.md` defines G01–G14 with acceptance criteria but no runner, test IDs, or evidence
schema. G04, G08, G09, G11 require hardware that is not present in CI. This is a design gap
to close before claiming anything, not a defect in intent.

---

## 5. Gate register (as recorded, unchanged)

| Gate | Description | Status |
|---|---|---|
| G01 | Source provenance | NOT RUN |
| G02 | Toolchain reproducibility | NOT RUN |
| G03 | AMD64 architecture | NOT RUN |
| G04 | CPU instruction dispatch | NOT RUN |
| G05 | Kernel build | NOT RUN |
| G06 | Boot and initialization | NOT RUN |
| G07 | Memory and process correctness | NOT RUN |
| G08 | AMD hardware qualification | NOT RUN |
| G09 | Graphics and compute | NOT RUN |
| G10 | Security controls | NOT RUN |
| G11 | OmniRed integration | NOT RUN |
| G12 | Performance measurement | NOT RUN |
| G13 | Regression and reliability | NOT RUN |
| G14 | Release readiness | NOT RUN |

---

## 6. Prioritized roadmap

Ordered by dependency, not preference. Each milestone states its exit evidence; a milestone is
not complete because its files exist.

**M0 — Repository hygiene (hours, no build)**
Fix F-05, F-06; add `.github/workflows/repo-integrity.yml` implementing CI Stage A (paths,
whitespace, links, SPDX presence); decide F-04 (move document or re-scope repository).
Exit: Stage A green on a PR; zero dead internal links.

**M1 — Pinned source and configuration (days)**
Add `kernel/source.lock` (upstream tag + commit + tarball SHA-256), `kernel/config/lxnu.config`,
`kernel/patches/` with README, and a container definition pinning Clang/LLVM.
Exit: lock file verifies; config parses with `make olddefconfig` in the pinned container.

**M2 — First independently buildable artifact (1–2 weeks)**
Build script producing `bzImage` + modules on an AMD64 runner; artifact SHA-256 and build
metadata recorded. This is the first milestone with a real binary.
Exit: G02 (reproducibility) and G05 (kernel build) evidence — two clean builds, matching
hashes, logs retained.

**M3 — Boot to userspace (2–4 weeks)**
QEMU boot with serial console, initramfs, `runit` as PID 1, minimal glibc userland.
Exit: G06 evidence — serial log from a reproducible image, boot target reached.

**M4 — Root and update architecture (weeks)**
EROFS lower + dm-verity + OverlayFS upper, A/B slots, Limine, installer skeleton.
Exit: signed image boots in QEMU; A/B rollback demonstrated with logs.

**M5 — Platform domains (months)**
OmniSilicon capability probe, performance libraries with scalar fallbacks and dispatch tests,
OmniRed policy prototype against supported kernel interfaces, Photon/Wayland session.
Exit: per-domain gates G08–G11 with hardware evidence on a real AMD64 machine.

Anything claiming System-One OS before M4 is unsupported. Anything claiming production
readiness before G14 is unsupported.

---

## 7. Risks

1. **Documentation outpacing engineering.** 4,640 lines of spec vs. 0 lines of code invites the
   impression that the system exists. The documents themselves warn against this; the
   repository layout does not.
2. **Ownership ambiguity (F-04).** Without a platform repository, cross-domain contracts have
   no review path.
3. **Build environment does not exist.** No AMD64 runner, no OBS project, no container image.
   Until that exists, every build claim is untestable.
4. **Hardware-dependent gates.** G04/G08/G09/G11 cannot be closed on hosted CI; they need
   real Ryzen/RDNA/XDNA hardware and a documented qualification matrix.

---

## 8. Audit limitations

- Static inspection only; no file was executed, compiled, or booted.
- No access to private repositories, runners, OBS projects, or hardware.
- GitHub API checks limited to public metadata at audit time.
- Findings describe the repository at `c05cfdb`; later commits may change them.

---

**Conclusion.** The specification is coherent; the implementation is absent. The next
engineering action is M0/M1, not another policy document. No component is claimed to ship, and
this audit does not change that.
