# Engineering Status Register

## 1. Purpose
This register records the engineering state of the platform and all major subsystems. It is a living status ledger and must distinguish between design, implementation, and demonstrated validity.

## 2. Status definitions
| Status | Meaning |
| --- | --- |
| Established | Architecture or policy decision has been made |
| Specified | Technical design and requirements have been documented |
| In Development | Implementation work is underway |
| Validated | Relevant tests have passed with recorded evidence |
| Qualified | Target hardware and production requirements have been demonstrated |
| Blocked | A dependency or unresolved issue prevents progress |
| Pending | Work has not yet been completed |

## 3. Status expectations
- Established: decisions that define the platform contract
- Specified: requirements and design details captured in subsystem docs
- Validated: measured evidence exists
- Qualified: hardware and workload requirements are proven in target environments
- Blocked/Pending: incomplete work remains explicitly visible

## 4. Governance note
The master specification defines status semantics. Subsystem documents must use the same status vocabulary to retain traceability across the architecture tree.

## 5. References
- SYSTEM-ONE-MASTER-SPEC.md
- ROADMAP.md
- subsystem engineering status sections throughout the repo
