# LXNU OmniSilicon Capability Discovery and Qualification Contract

Project: LXNU
Version: 1.6.6.2ɓ
Platform: System-One
Document status: Engineering foundation specification
Execution status: NOT RUN

1. Purpose

This document defines the hardware capability discovery and qualification contract for OmniSilicon.

OmniSilicon owns the model that reflects platform feature presence, runtime availability, and validation status. It must not equate hardware presence with validated support.

2. Mandatory Capability States

OmniSilicon must represent each capability with at least these states:
1. Present
2. Capable
3. Driver available
4. Runtime usable
5. Validated in scope

A system may discover a device without proving it is safe or correct to use for a given workload.

3. Core Responsibilities

OmniSilicon owns:
- processor and accelerator discovery
- CPU feature discovery
- GPU capability discovery
- NPU capability discovery when applicable
- topology and hardware relation reporting
- dependency on kernel and driver availability
- profile-aware capability models for AMD64 and ARM64

OmniSilicon does not own:
- kernel scheduling logic
- general userspace runtime service ownership
- workload orchestration policy
- optimized computational library implementation

4. Required Interface Contract

The capability model must provide:
- hardware identifier and topology data
- supported capability list
- selected profile association
- runtime availability status
- validation status and evidence source
- unsupported or unknown states
- failure and degraded-mode descriptions

5. Cross-Profile Rules

The OmniSilicon contract must be profile-aware:
- AMD64 Ryzen discovery rules are not implicitly valid for ARM64 Soundwave
- ARM64 discovery rules are not implicitly valid for AMD64 Ryzen
- GPU, NPU, firmware assumptions require explicit validation on the selected profile
- architecture-specific feature sets must be tracked separately

6. Validation Requirements

Capabilities are considered production-ready only after:
- hardware discovery is confirmed
- driver or kernel support is valid
- runtime usability is tested
- security and correctness are reviewed
- relevant functional or benchmark validation has been recorded

7. Failure Semantics

OmniSilicon must report one of the following outcomes:
- unknown
- unsupported
- unavailable
- degraded
- validated

It must never report a capability as usable based only on product naming or an implied platform assumption.

8. Validation Gates

OmniSilicon contract validation requires:
- discovery model review
- runtime usability checks
- architecture-specific profile handling review
- security and dependency review
- failure-state semantics review

Status: NOT RUN.

9. Current Status

This document defines the required OmniSilicon capability discovery and qualification contract for Phase 3. It does not claim qualified hardware, working drivers, or a validated platform.

Specified. NOT RUN. No gate measured. No component claimed to ship.
