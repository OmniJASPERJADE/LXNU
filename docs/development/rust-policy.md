Rust Engineering Policy

Project: LXNU / System-One
Status: Specification only — NOT RUN
Applies to: LXNU, OmniSoft, OmniRed, OmniSilicon, System-One Health, and suitable supporting services

1. Purpose

Rust is a strategic systems-programming language within the System-One engineering ecosystem.

Its adoption is intended to improve memory safety, concurrency safety, maintainability, and reliability where those benefits are appropriate to the component.

Rust complements C and C++. It does not replace them wholesale.

Language selection must be based on:

- Subsystem requirements and engineering constraints.
- Compatibility with Linux upstream interfaces.
- Hardware access and platform integration requirements.
- ABI and interoperability requirements.
- Measured performance and resource consumption.
- Long-term maintenance and available expertise.

Rust adoption is not itself evidence of improved performance, security, or implementation maturity.

2. Language Authority and Scope

The official stable Rust Reference is the primary authority for Rust language semantics.

Official Rust documentation, compiler documentation, Cargo documentation, and standard-library documentation govern their respective tools and interfaces.

Rust may be used where appropriate across:

- LXNU supporting components and services.
- OmniSoft runtime and platform services.
- OmniRed workload coordination and supporting services.
- OmniSilicon hardware discovery and qualification tools.
- System-One Health services.
- Build, validation, security, and system-management utilities.

Kernel-side Rust must remain compatible with the Rust support and toolchain requirements of the selected upstream Linux kernel revision.

No Rust component is considered implemented or shipped solely because this policy authorizes its use.

3. Production Toolchain Policy

Production Rust code MUST use the stable Rust toolchain.

Requirements:

- Pin the exact production Rust toolchain version.
- Record the compiler version and toolchain channel.
- Record host and target architecture information.
- Use controlled and reproducible toolchain upgrades.
- Prohibit nightly-only language or compiler features in production.
- Document any required compiler or target-specific configuration.
- Validate the selected toolchain against the component's build and test requirements.

A toolchain upgrade must be reviewed and validated before becoming the production default.

4. Minimum Supported Rust Version

Every Rust component MUST declare an explicit Minimum Supported Rust Version (MSRV).

The component must document:

- Its declared MSRV.
- The exact compiler version used for production builds.
- Supported target triples.
- Required standard-library and target support.
- Any component-specific compiler restrictions.

The declared MSRV must be tested.

Raising the MSRV is a compatibility-affecting engineering change and must be documented in the component's release notes and dependency policy.

A workspace must not silently inherit an undocumented MSRV.

5. C and C++ Coexistence

Rust adoption must preserve appropriate use of C and C++.

C remains appropriate for:

- Linux kernel interfaces and upstream-compatible kernel development.
- Existing low-level interfaces where C is the established contract.
- Hardware and driver integration where upstream requirements dictate C.

C++ remains appropriate for:

- Established graphics, media, and creator-tooling libraries.
- Existing performance-sensitive components with justified C++ architecture.
- Libraries and interfaces where C++ interoperability is the practical engineering choice.

Cross-language boundaries must be narrow, documented, and testable.

A subsystem must not be rewritten solely to increase the percentage of Rust code.

The selected language must serve the architecture rather than dictate it.

6. Dependency Governance

Rust dependencies are subject to the project's dependency-management, licensing, security, and reproducible-build policies.

Every dependency must be reviewed for:

- Purpose and necessity.
- Direct and transitive dependency exposure.
- License compatibility.
- Source provenance and maintenance status.
- Known vulnerabilities and security advisories.
- Build-time execution and procedural-macro behavior.
- Feature flags and unnecessary functionality.
- Compatibility with the component's MSRV.

Requirements:

- Maintain and review "Cargo.lock" for applicable production applications and workspaces.
- Use controlled dependency resolution.
- Avoid unpinned or floating Git dependencies in production.
- Review vendored dependencies and preserve required license notices.
- Minimize enabled dependency features.
- Record dependency changes in the component's engineering history.

A successful dependency build does not establish that the dependency is secure or suitable.

7. Unsafe Rust Policy

Safe Rust is the default.

Every use of "unsafe" MUST have a documented engineering justification.

Unsafe code must be:

- Minimized in scope.
- Encapsulated behind a safe interface where practical.
- Reviewed independently by a qualified reviewer.
- Tested against its documented safety invariants.
- Reassessed when surrounding interfaces or assumptions change.

Review must consider:

- Pointer validity, alignment, and provenance.
- Object lifetime and ownership.
- Aliasing and mutable-reference rules.
- Initialization and destruction.
- Data races and synchronization.
- Foreign-function interfaces.
- Interrupt, kernel, and execution-context assumptions where applicable.
- Buffer boundaries and memory access.
- Error and panic behavior.

Safety comments must explain the invariants that make the operation valid. Comments that merely restate the operation are insufficient.

Targeted tests and additional validation must accompany unsafe boundaries where practical.

8. FFI and ABI Policy

Foreign-function interfaces must have explicit and documented contracts.

Requirements:

- Declare calling conventions explicitly.
- Define ownership and lifetime rules for exchanged data.
- Validate pointers, lengths, and buffer boundaries.
- Define error propagation and failure behavior.
- Prevent unwinding across unsupported ABI boundaries.
- Document allocation and deallocation responsibilities.
- Version externally consumed interfaces where required.

Rust's default type layout must not be treated as a stable external ABI.

Use explicitly defined representation and interface contracts when crossing language or binary boundaries.

C, C++, and Rust components must not rely on undocumented assumptions about memory layout or ownership.

9. Error Handling, Concurrency, and Resource Management

Rust components must use deliberate error-handling strategies.

Requirements:

- Represent expected failures through explicit result or error types.
- Avoid panic as ordinary control flow.
- Document panic behavior at process, thread, and FFI boundaries.
- Define ownership and synchronization for shared state.
- Review cancellation, shutdown, and cleanup behavior.
- Prevent resource leaks and uncontrolled resource growth.
- Document concurrency assumptions and execution-context requirements.

Concurrency safety must be evaluated across the complete system boundary, not merely inferred from the use of Rust.

10. Build and Reproducibility

Rust builds must be reproducible within the project's defined build environment.

Record:

- Exact Rust toolchain version.
- Target triple and target configuration.
- Dependency lockfile and resolved dependency revisions.
- Enabled Cargo features.
- Build environment and relevant environment variables.
- Linker and native dependency inputs.
- Compiler and linker flags.
- Relevant build-script and procedural-macro inputs.

Build scripts and procedural macros must be reviewed because they execute code during the build process.

Dependency resolution must be controlled. Production builds must not silently acquire unreviewed dependency changes.

Reproducibility must be demonstrated through actual build comparisons; configuration alone is not proof.

11. Testing and Code Quality

Every production Rust component must define a test strategy appropriate to its responsibilities.

Expected validation includes:

- Unit tests.
- Integration tests.
- Interface and FFI tests.
- Malformed-input and boundary-condition tests.
- Concurrency and synchronization tests.
- Regression tests.
- Target-specific AMD64 testing.
- Formatting and lint checks.
- Dependency and license audits.
- Unsafe-code review.
- Build and reproducibility validation.

Tests must cover failure paths as well as expected operation.

Formatting and lint tools support code quality but do not establish correctness, security, or reliability.

Hardware-dependent components must be tested on the applicable hardware before hardware support is claimed.

12. Performance Engineering

Rust code must not receive presumed performance advantages merely because it is written in Rust.

Performance claims require measured evidence.

Benchmark records must identify:

- Hardware and CPU model.
- Operating-system and kernel revision.
- Compiler and toolchain versions.
- Workload and input characteristics.
- Baseline implementation.
- Test methodology and repeated measurements.
- Throughput, latency, and memory consumption as applicable.
- Correctness results.
- Relevant variance and environmental constraints.

AMD-specific optimization must preserve the validated x86-64-v3 baseline.

Optional x86-64-v4 or other instruction-set optimizations require runtime feature detection and safe fallback paths.

No optimization may introduce unsupported instruction requirements into the general production baseline.

Enabling a library, compiler feature, or optimization flag does not prove a speedup.

13. Security Requirements

Rust's memory-safety properties do not eliminate all security risks.

Security review must consider:

- Unsafe code and FFI boundaries.
- Input parsing and deserialization.
- Privilege transitions and authorization.
- Dependency and supply-chain exposure.
- Build scripts and procedural macros.
- Denial-of-service risks.
- Resource exhaustion.
- Error handling and information disclosure.
- Interaction with kernel and system security policies.

Security issues must be recorded, assessed, prioritized, and remediated through the project's security process.

14. Continuous Integration and Release Requirements

Production Rust components should be integrated into controlled CI workflows.

The intended CI checks include:

- Pinned stable toolchain.
- MSRV compatibility checks.
- Formatting validation.
- Lint checks.
- Unit and integration tests.
- Locked dependency resolution.
- Dependency, license, and vulnerability audits.
- Unsafe-code review requirements.
- Target-specific testing.
- Reproducibility checks where supported.

Release artifacts must identify the toolchain and dependency state used to produce them.

A CI configuration or documented workflow is not evidence that CI is operational. Successful execution logs are required before reporting a gate as passed.

15. Exceptions

Exceptions to this policy require written justification.

Each exception must identify:

- The affected component and requirement.
- The technical reason for the exception.
- Security, compatibility, and maintenance risks.
- Mitigation measures.
- Responsible engineering owner.
- Review date or expiration condition.

Convenience alone is not sufficient justification.

Exceptions must not silently become permanent project-wide policy.

16. Validation Status

The following gates remain unverified until actual evidence is produced:

Validation item| Status
Stable Rust toolchain qualification| NOT RUN
MSRV inventory| NOT RUN
Dependency and license audit| NOT RUN
Unsafe-code audit| NOT RUN
FFI and ABI audit| NOT RUN
Rust CI execution| NOT RUN
Reproducible Rust build| NOT RUN
AMD64 target validation| NOT RUN
Performance benchmarking| NOT RUN
Security validation| NOT RUN

No component is claimed to have passed these gates.

17. Governing Principle

Rust is a strategic engineering tool within System-One, not an ideological replacement for C or C++.

The project will select the language that best satisfies the subsystem's requirements, preserve clear interfaces, minimize unnecessary dependencies, and require measurable evidence before making implementation, security, or performance claims.

Specified. NOT RUN. No gate measured. No component claimed to ship.