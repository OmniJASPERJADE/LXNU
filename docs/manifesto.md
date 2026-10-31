# The LXNU Manifesto

## Build a better foundation. Do not imitate the past.

Computing should not force people to choose between freedom and refinement.

The industry has normalized complexity: disconnected components, fragmented experiences, unnecessary overhead, and systems that make users adapt to the machine.

LXNU exists to challenge that status quo.

## One platform. One experience. Engineered end to end.

LXNU is the kernel foundation of System-One. It uses the proven Linux kernel as its engineering foundation and applies carefully selected XNU-inspired architectural principles.

It does not contain Mach source code or Apple code. It is not a macOS clone.

Its purpose is to make a powerful, open, dual-architecture computing platform feel coherent.

## Our principles

### 1. Integration is a discipline
Hardware, kernel interfaces, userspace, graphics, storage, security, and applications must work together through explicit contracts.

### 2. Complexity belongs beneath the experience
The engineering may be sophisticated. The experience should remain understandable.

### 3. Performance must be measured
No speedup is real until it is demonstrated through reproducible benchmarks and validation.

### 4. Freedom requires responsibility
Open foundations, transparent decisions, auditable changes, and respect for upstream projects are essential.

### 5. Build only what earns its place
Every subsystem must justify its complexity, resource consumption, maintenance cost, and security impact.

## The engineering standard

- AMD64-first platform engineering.
- Linux upstream as the kernel foundation.
- Stable and documented interfaces.
- Security designed into architecture.
- Reproducible builds and traceable source provenance.
- C and C++ where appropriate; stable Rust where it improves safety and maintainability.
- No unsupported performance claims.
- No implementation claims without evidence.

## The ambition

We are not building another distribution with a new wallpaper.

We are building the foundation for a unified computing platform: powerful enough for creators, deliberate enough for professionals, and open enough for developers to shape.

**The freedom to build. The discipline to make it feel simple.**

---

*LXNU — A System-One engineering project.*

*Current status: Specification and architecture work. Implementation and validation must be independently demonstrated.*