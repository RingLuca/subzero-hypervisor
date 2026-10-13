# SubZero: Bare-Metal x86_64 Hypervisor & Virtualization Research Framework

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Architecture: x86__64](https://img.shields.io/badge/Arch-x86__64-orange.svg)]()
[![VT-x / SVM](https://img.shields.io/badge/Virtualization-Intel%20VT--x%20%7C%20AMD--V-green.svg)]()

A modular, lightweight Ring -1 virtualization research framework and hypervisor SDK for Windows and bare-metal x86_64 environments. Designed for hardware-assisted virtualization research, nested paging analysis (EPT/NPT), hypercall interfaces, and hardware intercept telemetry.

---

## ⚡ Core Architecture

```
                  ┌─────────────────────────────────────────┐
                  │          Guest OS (Ring 0 / Ring 3)     │
                  └────────────────────┬────────────────────┘
                                       │ VM-Exit (Trap)
                                       ▼
    ┌─────────────────────────────────────────────────────────────────────┐
    │              SubZero Hypervisor Core (Ring -1 VMM)                  │
    ├───────────────────┬───────────────────┬─────────────────────────────┤
    │  VMCS / VMCB Mgt  │   EPT / NPT MMU   │    Intercept Handlers       │
    │  - State setup    │   - 4-Level walk  │    - CPUID / MSR Bitmaps    │
    │  - Controls mask  │   - Identity map  │    - I/O Port trapping      │
    │  - Guest context  │   - Split pages   │    - TSC Timing cloaking    │
    └───────────────────┴───────────────────┴─────────────────────────────┘
```

## 🛠️ Repository Structure

- `include/`: Hardware virtualization structures, MSR definitions, and VMCS/VMCB field encodings.
- `src/vtx/`: Intel VT-x execution logic (VMXON, VMCS configuration, EPT paging, VM-exit dispatch).
- `src/svm/`: AMD-V (SVM) control area structures and intercepts.
- `src/intercepts/`: Hardware traps (MSR bitmaps, I/O bitmaps, CR shadows, CPUID emulation).
- `src/diagnostics/`: Telemetry, VM-exit qualifier decoding, and state dumping.
- `src/benchmarks/`: Micro-benchmarks for VM-exit roundtrip latency.

## 🤝 Community & Contributions
SubZero is developed modularly by systems researchers. Contributions to hardware intercept handlers, paging algorithms, and diagnostic modules are welcome via pull requests.
