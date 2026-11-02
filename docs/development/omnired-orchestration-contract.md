# LXNU OmniRed Orchestration Contract

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Document status: Engineering foundation specification
Execution status: NOT RUN

1. Purpose

This document defines the engineering contract for OmniRed, the workload orchestration and resource coordination domain.

OmniRed does not own the kernel scheduler, hardware discovery, or device implementation. It coordinates workload policy and resource placement through supported interfaces.

2. Owned Responsibilities

OmniRed owns:
- workload classification
- placement policy
- resource coordination
- policy-based orchestration
- power and thermal coordination logic
- workload monitoring signals
- conflict handling between competing workloads

OmniRed does not own:
- kernel scheduling ownership
- device driver ownership
- low-level hardware discovery
- direct hardware control of accelerators

3. Interface Model

OmniRed must consume and produce interfaces with:
- versioned policies
- explicit data structures
- workload metadata
- capacity and capability inputs
- placement decisions and rationale
- failure and fallback states

Required inputs:
- capability model from OmniSilicon
- runtime environment from System-One OS
- kernel scheduling and resource constraints from LXNU
- workload metadata supplied by user and service domains

Required outputs:
- placement policy output
- resource allocation intention
- performance-policy guidance
- health and conflict signals

4. Scheduler Boundary

OmniRed may influence placement and workload strategy, but it must not replace or bypass the Linux scheduler.

Requirements:
- scheduling remains owned by LXNU
- OmniRed acts on policy and orchestration decisions, not kernel scheduling definitions
- no direct manipulation of kernel internals
- any required kernel-facing interface must be reviewed and approved by LXNU

5. Cross-Profile Behavior

OmniRed must behave per selected profile and must not assume AMD hardware is present on ARM64.

Required rules:
- capability records must come from OmniSilicon
- workload eligibility must be checked against actual profile capabilities
- unsupported accelerators must be treated as unavailable or unsupported, not assumed
- policy logic must be architecture-neutral in public form

6. Security and Failure Handling

OmniRed policies must include:
- least-privilege access to resource metadata
- explicit handling for degraded capability states
- rollback or fallback behavior when a placement target becomes unavailable
- policy logs and diagnostic outputs
- conflict and failure escalation paths

7. Validation Gates

OmniRed contract validation requires review of:
- placement and resource policy design
- supported interface compatibility
- kernel boundary compliance
- security boundary definition
- profile-specific capability handling
- failure and fallback behavior

Status: NOT RUN.

8. Current Status

This document defines the required OmniRed orchestration contract for Phase 3. It is not evidence of workload execution, hardware validation, or production integration.

Specified. NOT RUN. No gate measured. No component claimed to ship.
