<!-- 
SEO METADATA & KEYWORDS (Invisible to readers, visible to Google Crawlers)
Keywords: IW Cyber Ops, Muhammad Imran Wakeel, Systems C Programming, x86-64 Assembly Matrix, ARM64 Assembly, Hardware Security Frontier, Digital Logic Circuits, Logisim ALU, Human Matrix Social Engineering, Cognitive Exploitation, Low Level Systems Engineering, Vulnerability Research, The 60-30-10 Rule, Reverse Engineering Foundations.
-->

# 🛠️ IW Core Tracks — The Sovereign Shadow Pillars

> **System Operator & Architect:** Muhammad Imran Wakeel (`@iwcyberops`)  
> **Repository Scope:** Permanent, Daily Continuous Systems Engineering & Cognitive Research (M01 – M42)  
> **Ecosystem Alignment:** Foundational Engine of `IW-Mission-Control` & `IW-Knowledge-Base`

---

## 🏛️ Executive Philosophy: The Immutability of Core Mechanics

Roadmaps change, high-level offensive frameworks evolve, and software tools become obsolete within years—**but the laws of computation, silicon physics, and human cognitive psychology are immutable.**

`IW-Core-Tracks` represents the **Sovereign Foundation** of the entire 42-month apex security journey. While monthly domains in `IW-Knowledge-Base` shift from Web to Active Directory, Hypervisors, and Fuzzing, these **Four Continuous Tracks** run in parallel every single day for 1,260+ consecutive days (~12 Focused Hours/Day).

This repository is where theory meets bare-metal reality. We do not just read about pointers—we engineer custom memory allocators. We do not just look at decompiled code—we decode raw CPU opcodes and register states. We do not stop at software—we build ALUs, probe SPI flash chips, and analyze the psychological attack surface of the human mind.

---

## 🏗️ The Four Sovereign Pillars of Mastery

```
                     ┌────────────────────────────────────────────────────────┐
                     │          IW CORE TRACKS (THE 4 SHADOW PILLARS)         │
                     └───────────────────────────┬────────────────────────────┘
                                                 │
        ┌───────────────────┬────────────────────┼───────────────────┬───────────────────┐
        │                   │                    │                   │                   │
  ┌─────▼─────────────┐ ┌───▼──────────────┐ ┌───▼─────────────┐ ┌───▼─────────────┐
  │   01. SYSTEMS C   │ │  02. ASSEMBLY    │ │  03. HARDWARE   │ │  04. HUMAN      │
  │   & C++ TRACK     │ │  & RE MATRIX     │ │  FRONTIER       │ │  MATRIX         │
  └───────────────────┘ └──────────────────┘ └─────────────────┘ └─────────────────┘
```

---

### 1. ⚙️ Pillar I: Systems C / C++ Track (The Mother Language)
*Daily Dedicated Engine: 1.0 Hour / Day | 42-Month Multi-Tier Progression*

The language in which modern infrastructure, operating systems, and exploit primitives are authored. Mastery demands treating memory as a raw array of bytes.

* **M01–M03 (Syntax, Memory & Pointers):** Pure C99 dynamic data structures from scratch (linked lists, hash tables, dynamic arrays), pointer arithmetic, array-pointer duality, and memory alignment padding.
* **M04–M06 (Dynamic Memory & POSIX APIs):** Multi-process programming with `fork()`, `execve()`, socket servers, POSIX shared memory, custom memory allocators, and memory leak analysis with Valgrind.
* **M07–M09 (Systems C, Compilers & Linkers):** POSIX threads (`pthreads`), mutexes, condition variables, atomic operations, parsing raw ELF section headers, and authoring shared libraries.
* **M10–M15 (C++ Object Model & Safety):** Virtual method tables (`__vptr`/vtable), multiple inheritance memory offsets, smart pointers (`std::shared_ptr`, `std::unique_ptr`), RAII, move semantics, and Use-After-Free patterns.
* **M16–M21 (Embedded C & Kernel Code):** Linux kernel module programming, character device drivers, managing slab/slub allocations, and custom QEMU virtual device models.
* **M22–M27 (Parsers, Harnesses & Sanitizers):** Memory-safe binary parsers, high-performance LibFuzzer test harnesses, and analyzing AddressSanitizer (ASan) shadow memory.
* **M28–M35 (Modern C++ & Engine Sources):** Line-by-line manual code audit of complex open-source engines (Google V8, JavaScriptCore, Chromium Mojo, Linux kernel).
* **M36–M42 (Research Tooling & Upstream Patches):** Engineering custom grammar-aware fuzzing mutators, authoring upstream Linux/Chromium security patches, and building Clang AST static analysis tools.

---

### 2. 🔌 Pillar II: Assembly & Reverse Engineering Matrix (The Machine's Soul)
*Daily Dedicated Engine: 1.0 Hour / Day | Decoding Opcodes & Dynamic Disassembly*

Decoding the raw instruction streams executed by the processor. When source code is unavailable, assembly is the absolute ground truth.

* **M01–M03 (x86-64 Registers & Instructions):** Data movement (`mov`, `movzx`, `movsx`, `lea`), stack operations (`push`, `pop`), arithmetic/logic instructions, and flags register (`ZF`, `CF`, `SF`, `OF`).
* **M04–M06 (ABI & Calling Conventions):** System V AMD64 vs. Microsoft x64 calling conventions, stack frame initialization, parameter registers, and manual disassembly reading.
* **M07–M09 (Compiler Output Reversing):** Reconstructing high-level C logic from unoptimized (`-O0`) and heavily optimized (`-O2`, `-O3`, `-Os`) assembly dumps.
* **M10–M15 (Advanced x86-64 & ARM64 Intro):** Reversing polymorphic C++ vtables, solving CrackMes, ARM64 register layouts (`X0–X30`), and instruction decoding (`LDR`, `STR`, `STP`, `LDP`, `BL`, `RET`).
* **M16–M21 (Mobile & Embedded RE):** Reversing ARM64 Android `.so` native JNI libraries, and decompiling stripped MIPS/ARM embedded IoT firmware binaries.
* **M22–M27 (Advanced Binary Analysis):** Decompiler correction in Ghidra, identifying control-flow flattening obfuscation, and writing automated Ghidra scripts in Python.
* **M28–M35 (Specialized Assembly):** Tracing JIT-compiled native machine code in memory, analyzing hypervisor VM exit routines, and low-level context switches.
* **M36–M42 (Research-Grade RE):** Deconstructing complex closed-source enterprise targets, binary patch diffing with BinDiff, and microarchitectural security analysis.

---

### 3. ⚡ Pillar III: Hardware Frontier (The Physical & Silicon Layer)
*Daily Dedicated Engine: 1.0 Hour / Day | From Logic Gates to Physical Side-Channels*

Bridging the gap between software abstraction and physical silicon. Software vulnerabilities are born on copper traces and silicon transistors.

* **M01–M03 (Digital Electronics Fundamentals):** Ohm’s Law, Kirchhoff’s Laws, discrete logic gates (AND, OR, XOR, NOT), RS Latches, D Flip-Flops, and building a functional 4-bit ALU inside the Logisim simulator.
* **M04–M06 (CPU Architecture & Memory):** CPU instruction pipelining (Fetch, Decode, Execute, Memory, Writeback), cache hierarchies (L1/L2/L3), MMU, page tables, TLB, hardware interrupts, and DMA mechanics.
* **M07–M09 (Embedded Hardware Interfaces):** Microcontrollers vs. MPUs, Memory-Mapped I/O (MMIO), Port I/O, clock signals, and serial bus protocols.
* **M10–M15 (Hardware Debug Protocols):** UART pinout identification via multimeter/logic analyzer, SPI flash chip dumping using CH341A/FTDI, and I2C bus decoding.
* **M16–M21 (JTAG, Firmware & Boot Chains):** JTAG boundary scan TAP state machines, U-Boot bootloader mechanics, UEFI architecture, TPM registers, and Secure Boot trust chains.
* **M22–M27 (Hardware-Assisted Security):** Intel VMX / AMD SVM virtualization extensions, TPM platform configuration registers (PCRs), and ARM TrustZone hardware isolation.
* **M28–M35 (Microarchitecture & Timing Channels):** Out-of-order execution, speculative execution pipelines, branch predictors (BPU/BTB), and measuring cache latencies via `RDTSC` (Spectre/Meltdown).
* **M36–M42 (Physical Attack Surfaces):** Hardware-level side channels, power analysis fundamentals, fault injection concepts, and physical voltage/clock glitching.

---

### 4. 🧠 Pillar IV: The Human Matrix (Cognitive & Psychological Exploitation)
*Continuous Analytical Thread | The Human Subsystem & Operational Mindset*

The human operator is the only component in an infrastructure that cannot be patched with software updates.

* **Cognitive Bias Weaponization:** Analyzing heuristics and biases (Authority, Scarcity, Social Proof, Consistency) to engineer pretext scenarios and social engineering attack vectors.
* **Psychological OSINT & Behavioral Profiling:** Extracting actionable intelligence from digital footprints, linguistic patterns, organizational hierarchies, and decision-making friction points.
* **Influence & Deception Mechanics:** Deconstructing elicitation techniques, non-verbal communication cues, and micro-expression analysis during high-assurance physical red teaming.
* **Operational Mindset & Resilience:** Engineering personal cognitive discipline, sustaining 12-hour high-intensity research blocks without burnout, eliminating imposter syndrome, and maintaining absolute operational security (OPSEC).

---

## 📂 Repository Directory Tree

```text
IW-Core-Tracks/
│
├── README.md                           <-- Sovereign Master Architecture Index
│
├── 01-systems-c/                       <-- C99, POSIX, Allocators, Sockets, Kernel Modules
│   ├── README.md
│   └── ...
│
├── 02-assembly-matrix/                 <-- x86-64, ARM64, Ghidra Decompilation, Opcodes
│   ├── README.md
│   └── ...
│
├── 03-hardware-frontier/               <-- Logisim ALUs, Bus Protocols (UART/SPI), CPU Microarch
│   ├── README.md
│   └── ...
│
└── 04-human-matrix/                    <-- Cognitive Biases, Social Engineering, OPSEC Mindset
    ├── README.md
    └── ...
```

---

## 🧭 The 60/30/10 Rule of Technical Mastery

Every research artifact in this repository adheres to the **IW Research Standard**:

| Ratio | Pillar Domain | Daily Application |
| :---: | :--- | :--- |
| **60%** | **Hands-on Implementation (7.2h/day)** | Writing C code from scratch, crafting raw assembly stubs, building circuits in Logisim, debugging crashes in GDB. |
| **30%** | **Theoretical Ingestion (3.6h/day)** | Reading official architecture reference manuals (Intel SDM, ARM ARM), RFC specifications, and peer-reviewed academic papers. |
| **10%** | **Knowledge Engineering (1.2h/day)** | Producing structured Markdown documentation, architectural flowcharts, and maintaining clean git history. |

---

## 🌐 The IW Cyber Ops Ecosystem

This repository forms a vital component of the four-tier **IW Cyber Ops Architecture**:

* 🛰️ **[`IW-Mission-Control`](https://github.com/iwcyberops/IW-Mission-Control):** Overarching 42-Month Master Roadmap, Daily Live Logs, and Official PDF Releases.
* 📚 **[`IW-Knowledge-Base`](https://github.com/iwcyberops/IW-Knowledge-Base):** Deep monthly technical documentation across all 5 operational phases.
* 🛠️ **[`IW-Core-Tracks`](https://github.com/iwcyberops/IW-Core-Tracks):** *[Current Repo]* The 4 continuous side tracks (C, Assembly, Hardware, Human Matrix).
* ⚔️ **[`IW-Arsenal`](https://github.com/iwcyberops/IW-Arsenal):** Custom exploit harnesses, tools, fuzzers, and the 27 Master Portfolio projects.

---

## 📜 The Sovereign Truth

$$\text{Mechanisms} > \text{Tools} \quad \Big\vert \quad \text{Source Code} > \text{Interfaces} \quad \Big\vert \quad \text{Silicon} > \text{Abstractions}$$

> *"Hacking is not a collection of tools; it is an absolute depth of computational understanding. If you master the core, the surface becomes completely transparent."*

<br>

**Founder & Lead Researcher:** **Muhammad Imran Wakeel** (`@iwcyberops`)  
**Mission Scope:** Apex Vulnerability Research & Systems Engineering (2026 – 2029)  
*All research conducted strictly within owned lab environments, isolated VMs, or authorized disclosure scopes.*
