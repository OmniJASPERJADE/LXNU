# LXNU Omni Performance Libraries Dispatch and Fallback Contract

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Document status: Engineering foundation specification
Execution status: NOT RUN

1. Purpose

This document defines the engineering contract for Omni Performance Libraries.

The libraries own optimized computational operations, runtime-safe dispatch, and fallback behavior. They must remain architecture-aware without substituting for kernel scheduling, hardware qualification, or workload orchestration ownership.

2. Ownership Boundary

Omni Performance Libraries owns:
- optimized computational operations
- SIMD and vectorized execution paths
- runtime dispatch policy
- architecture-specific compatibility checks
- scalar fallback paths
- correctness and performance validation metadata

Omni Performance Libraries does not own:
- kernel scheduling
- hardware discovery ownership
- general service lifecycle
- application orchestration policy

3. Dispatch Model

Each optimized path must define:
- supported architecture and profile
- required feature set
- runtime detection mechanism
- fallback path
- error or degraded-state handling
- validation evidence scope

Requirements:
- unsupported instructions must not be executed through a blind assumption
- dispatch decisions must be explicit and validated
- fallback behavior must be documented and tested
- ARM64 and AMD64 dispatch rules must remain independent

4. Correctness and Safety Rules

Optimized implementations must preserve correctness and must not bypass runtime checks.

Required safety properties:
- memory-safe handling of dispatch inputs
- explicit feature detection before optimized execution
- fallback to generic or scalar implementations when required
- no implicit microarchitecture assumptions without detection and validation

5. Cross-Profile Boundary

The dispatch model must treat AMD64 and ARM64 separately.

Rules:
- AMD64 instruction-set baselines and optimized dispatch paths are not portable to ARM64 without explicit validation.
- ARM64 dispatch must use architecture-specific detection and support rules.
- Cross-profile capability assumptions are invalid in public contracts.

6. Validation Gates

The dispatch contract requires validation of:
- capability detection logic
- fallback behavior
- feature and memory correctness
- architecture-specific compatibility
- benchmark and validation documentation

Status: NOT RUN.

7. Current Status

This document defines the required Omni Performance Libraries dispatch and fallback contract for Phase 3. It does not claim optimized execution success, measured performance, or production release readiness.

Specified. NOT RUN. No gate measured. No component claimed to ship.
