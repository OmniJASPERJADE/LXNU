Contributing to LXNU

Thank you for your interest in contributing to LXNU.

LXNU is an independent Linux kernel engineering project for System-One. It applies selected XNU-inspired architectural principles while retaining Linux upstream as its kernel foundation.

Contributions must preserve the project's architectural direction, technical integrity, and commitment to measurable results.

1. Before Contributing

Before proposing a change:

- Read the "LXNU Manifesto" (docs/manifesto.md).
- Read the "Architecture Overview" (docs/architecture/overview.md).
- Review the "Security Policy" (SECURITY.md).
- Check existing issues and discussions for related work.

Do not assume that a proposed feature has been approved simply because it appears in a discussion.

2. Architectural Principles

Contributions must follow these principles:

- AMD64 is the production architecture target.
- Linux upstream remains the kernel foundation.
- LXNU must not duplicate established Linux functionality without justification.
- System components must have clearly defined ownership.
- Interfaces and dependencies must be documented.
- Security and reliability take priority over unnecessary complexity.
- Performance claims require reproducible measurements.
- Unimplemented specifications must not be presented as completed features.

3. Upstream Linux Compatibility

Kernel-related contributions must identify:

- The exact upstream Linux revision involved.
- Whether the change is upstream, downstream, or proposed for upstream submission.
- Why a downstream modification is necessary.
- Any compatibility or maintenance consequences.

Keep downstream patches separate and traceable.

Do not remove upstream copyright notices or SPDX identifiers.

4. Programming Languages

Use the language appropriate to the component.

- C: Linux kernel integration and established kernel subsystems.
- C++: Suitable supporting components and performance-oriented software.
- Rust: Appropriate system services, tooling, and components where memory safety and maintainability justify its use.

Production Rust must use stable toolchains and an explicit MSRV policy.

Rust contributions require dependency review, license auditing, reproducible builds, testing, and additional scrutiny for unsafe code.

5. Code Quality

Contributions should:

- Follow established project and upstream conventions.
- Use descriptive names and maintainable interfaces.
- Avoid unnecessary dependencies.
- Handle errors explicitly.
- Include relevant tests.
- Document non-obvious design decisions.
- Avoid unsupported hardware assumptions.
- Preserve safe fallback behavior where required.

Security-sensitive changes require additional review.

6. Testing and Validation

A contribution should identify the tests required to validate it.

Depending on scope, testing may include:

- Compilation and static analysis.
- Unit and integration tests.
- Kernel configuration validation.
- Hardware compatibility testing.
- Boot testing.
- Security testing.
- Performance benchmarking.
- Regression testing.

A successful compilation does not prove runtime correctness.

A benchmark result must identify its hardware, software configuration, workload, methodology, and reproducibility conditions.

Unexecuted tests must remain marked NOT RUN.

7. Pull Requests

Pull requests should include:

1. A concise description of the change.
2. The problem being addressed.
3. The architectural justification.
4. A list of affected components.
5. Dependencies and compatibility considerations.
6. Tests performed and their results.
7. Known limitations and outstanding risks.

Keep changes focused. Large architectural changes should be discussed before implementation.

8. Licensing and Source Provenance

Contributions must respect the repository's existing license and the licensing requirements of every affected upstream or third-party component.

Do not submit copied proprietary source code, undocumented third-party code, or material without appropriate usage rights.

Include appropriate copyright and SPDX information.

9. Review and Acceptance

A contribution is not accepted merely because it builds.

Changes must be reviewed for correctness, maintainability, security, architectural consistency, and validation evidence.

The project may reject changes that introduce unjustified complexity, duplicate upstream functionality, weaken security, or make unsupported claims.

10. Current Project Status

LXNU 1.6.6.2ɓ remains an architectural specification and engineering project.

No production implementation or completed validation is claimed.

Contributors should distinguish clearly between proposed, specified, implemented, tested, and verified work.

Specified. NOT RUN. No gate measured. No component claimed to ship.

---

LXNU — Build with purpose. Engineer with evidence.