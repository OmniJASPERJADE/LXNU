LXNU Licensing and Source Provenance

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Document status: Licensing policy specification

1. Purpose

LXNU is built on the upstream Linux kernel and incorporates independently developed architecture, integration, configuration, and supporting software.

This document establishes the project's licensing and source-provenance principles.

LXNU must respect the legal rights and licensing requirements of upstream projects, contributors, and third-party dependencies.

2. Repository License

The repository currently contains a root "LICENSE" file identifying GNU General Public License version 2.

That existing license file must be preserved unless a deliberate, documented licensing decision authorizes a change.

The presence of the root license does not mean that every third-party component, imported source file, binary, or dependency automatically has identical licensing terms.

3. Linux Kernel Licensing

LXNU uses the upstream Linux kernel as its foundation.

Linux kernel source is generally distributed under GPL-2.0-only, with individual files and components retaining their applicable licensing notices.

LXNU must:

- Preserve upstream copyright notices.
- Preserve existing SPDX identifiers.
- Retain applicable license texts.
- Document modified upstream files.
- Identify downstream patches.
- Respect redistribution and source-disclosure obligations.
- Avoid claiming ownership of upstream Linux code.

The exact licensing status of a file must be determined from its applicable source notices and provenance.

4. Third-Party Components

Every imported dependency must be evaluated independently.

The project must record:

- Component name and version.
- Original source repository.
- Upstream license.
- Copyright and attribution requirements.
- Modification status.
- Redistribution obligations.
- Security and maintenance status.

Dependencies without established provenance or acceptable licensing terms must not be silently incorporated.

5. SPDX and Copyright Requirements

Source files should retain their original SPDX identifiers.

New source files should include an appropriate SPDX identifier and copyright notice where required.

SPDX identifiers must accurately reflect the applicable license. Contributors must not assign licenses merely for convenience.

6. Downstream Modification Policy

LXNU-specific modifications to upstream Linux must remain identifiable.

Each downstream patch should document:

1. The affected upstream component.
2. The original upstream revision.
3. The reason for the modification.
4. The technical changes.
5. The licensing implications.
6. Whether upstream submission is intended.

Avoid unnecessary forks of upstream code.

Prefer maintainable patches and documented integration interfaces.

7. Rust, C, and C++ Dependencies

Language choice does not remove licensing obligations.

Rust crates, C libraries, C++ libraries, build tools, and generated code must undergo dependency and license review.

Production dependency management must include:

- Version pinning.
- Source provenance.
- License compatibility review.
- Security vulnerability review.
- Reproducible build considerations.
- Documentation of exceptions.

8. Binary and Package Distribution

Redistributed binaries and packages must retain applicable notices and comply with their component licenses.

System-One package metadata should identify relevant source packages and license information.

Where source redistribution or written offers are required, the project must satisfy the applicable obligations.

9. Documentation and Branding

LXNU and System-One project names identify this independent engineering effort.

The project does not claim endorsement, ownership, or affiliation with Apple or the Linux Foundation.

References to Linux, AMD, Rust, and other upstream technologies identify their respective projects or products and do not imply endorsement.

10. Licensing Review

Before a release, the project should conduct a licensing audit covering:

- Kernel source.
- Downstream patches.
- Userspace components.
- Build dependencies.
- Rust dependencies.
- Binary redistributions.
- Documentation and bundled assets.

Unresolved licensing issues must be documented and must block affected distributions when legal compliance cannot be established.

11. Current Status

This document establishes licensing policy. It is not a completed legal audit or certification of every repository file.

The existing root "LICENSE" file remains in place.

Specified. NOT RUN. No complete dependency audit claimed. No blanket third-party license assumed.

---

LXNU — Respect the source. Preserve the freedom to build.