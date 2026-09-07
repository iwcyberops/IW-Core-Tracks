<!-- 
SEO METADATA & KEYWORDS (Invisible to readers, visible to Google Crawlers)
Keywords: IW Cyber Ops, Muhammad Imran Wakeel, OverTheWire Leviathan Solutions, Leviathan Wargame Walkthrough, Linux Privilege Escalation, ltrace Dynamic Tracing, strace System Calls, SUID Binary Exploitation, Symlink Attacks, Reverse Engineering Wargames, Cybersecurity Knowledge Base.
-->

# 🐉 02: OverTheWire Leviathan — Binary Auditing & Privilege Escalation

> **Knowledge Base Directory:** `IW-Core-Tracks/05-wargames-and-ctfs/02-leviathan`  
> **System Operator & Lead Researcher:** Muhammad Imran Wakeel (`@iwcyberops`)  
> **Platform Target:** [overthewire.org/wargames/leviathan](https://overthewire.org/wargames/leviathan.html)  
> **Host / Port:** `ssh leviathan0@leviathan.labs.overthewire.org -p 2223`  
> **Mission Objective:** Transition from pure Linux administration into runtime binary auditing, dynamic system call inspection, and local privilege escalation (LPE).

---

## 🏛️ The Tactical Imperative of Leviathan

If **Bandit** is the bootcamp of Linux system navigation, **Leviathan is the gateway to binary reverse engineering and privilege escalation.**

In real-world red teaming and systems research, target servers frequently contain custom compiled helper utilities and proprietary SUID binaries. These applications run with elevated administrative privileges but often harbor critical logic flaws: unquoted variable inputs, insecure file path checks, reliance on hardcoded credentials, and race windows between file access checks and execution.

Leviathan forces a researcher to look under the hood of compiled C binaries without having access to the original source code. Instead of guessing, we use dynamic tracing tools—**`ltrace`** (to intercept shared library calls like `strcmp` and `printf`) and **`strace`** (to monitor kernel system calls like `open`, `read`, and `execve`). By intercepting runtime execution at the syscall boundary, we expose hardcoded secrets and manipulate file descriptors to seize elevated privileges.

This directory serves as the **IW Cyber Ops Wargame Ledger** for the Leviathan series, documenting the complete vulnerability analysis and command traces for all 8 levels (Levels 0 through 7).

---

## 🧠 Core Attack Vectors Mastered in Leviathan

The challenges in this series teach the foundational mechanics of binary vulnerability discovery:

```
                  ┌────────────────────────────────────────────────────────┐
                  │            LEVIATHAN TACTICAL ATTACK VECTORS           │
                  └───────────────────────────┬────────────────────────────┘
                                              │
         ┌───────────────────┬────────────────┴───────────────────┬───────────────────┐
         │                   │                                    │                   │
   ┌─────▼─────────────┐ ┌───▼──────────────┐           ┌─────────▼─────────┐ ┌───────▼─────────────┐
   │ 1. DYNAMIC        │ │ 2. SYMLINK &     │           │ 3. PARAMETER      │ │ 4. LOCAL BRUTE-     │
   │    TRACING        │ │    PATH HIJACK   │           │    INJECTION      │ │    FORCE LOOPS      │
   │  (ltrace/strace)  │ │    (ln -s)       │           │  (access vs exec) │ │   (Bash One-Liners) │
   └───────────────────┘ └──────────────────┘           └───────────────────┘ └─────────────────────┘
```

1. **Dynamic Shared Library Tracing (`ltrace`):** Hooking into user-space library calls to inspect memory buffers, exposing plaintext passwords directly passed into string comparison functions (`strcmp`, `strncmp`).
2. **Kernel System Call Tracing (`strace`):** Intercepting low-level kernel transitions (`openat`, `stat`, `access`, `execve`) to identify hardcoded temporary file paths and unhandled error states.
3. **Insecure Path Handling & Parameter Injection:** Exploiting flawed logic where binaries pass unsanitized filenames to shell wrappers (`system("/bin/cat " + file)`), enabling arbitrary argument injection and file reading via space-separated paths.
4. **Symbolic Link (Symlink) Redirection:** Weaponizing `ln -s` to redirect hardcoded file reads in SUID binaries toward restricted password files (`/etc/leviathan_pass/`).
5. **Automated Local Brute-Forcing:** Writing high-speed, headless Bash loops to brute-force 4-digit PIN verification routines on local SUID executables.
6. **Binary-to-ASCII Stream Decoding:** Reconstructing raw binary bit streams (`01100001...`) into readable ASCII credential artifacts.

---

## 📊 Leviathan Level Progression Matrix

| Level Target | Core Vulnerability / Topic | Primary Tool / Technique | Level Status | Detailed Notes |
| :--- | :--- | :--- | :---: | :--- |
| **Level 0 ➔ 1** | Hidden Directory Data Mining | `grep -rn`, Hidden Bookmarks | 🟢 Solved | `[leviathan.md#level-0--1](./leviathan.md)` |
| **Level 1 ➔ 2** | Plaintext `strcmp` Memory Exposure | `ltrace` Library Call Interception | 🟢 Solved | `[leviathan.md#level-1--2](./leviathan.md)` |
| **Level 2 ➔ 3** | Parameter Injection in `system()` | Filename Spaces & Path Expansion | 🟢 Solved | `[leviathan.md#level-2--3](./leviathan.md)` |
| **Level 3 ➔ 4** | Hardcoded Password Validation | `ltrace` Dynamic Secret Sniffing | 🟢 Solved | `[leviathan.md#level-3--4](./leviathan.md)` |
| **Level 4 ➔ 5** | Binary Bitstream Output | Base-2 (Binary) to ASCII Converter | 🟢 Solved | `[leviathan.md#level-4--5](./leviathan.md)` |
| **Level 5 ➔ 6** | Hardcoded Temp File Access | Symlink Redirection (`ln -s`) | 🟢 Solved | `[leviathan.md#level-5--6](./leviathan.md)` |
| **Level 6 ➔ 7** | 4-Digit Numeric PIN Validation | Bash Brute-Force One-Liner Loop | 🟢 Solved | `[leviathan.md#level-6--7](./leviathan.md)` |
| **Level 7 ➔ Conquered** | Final Privilege Verification | Full Wargame Conquered | 🟢 Completed | `[leviathan.md#level-7--complete](./leviathan.md)` |

---

## 📂 Directory Walkthrough File

All 8 levels of Leviathan are recorded with full command traces and technical explanations inside the master document:

* 📄 **[`leviathan.md`](./leviathan.md):** Complete, step-by-step technical walkthrough from Level 0 to Level 7.

---

## 🛡️ About the Author

**Muhammad Imran Wakeel** is an independent systems researcher and the Founder of **IW Cyber Ops**. This practical wargame repository is an active component of a 42-month master plan engineered for absolute computational foundations and high-impact vulnerability research.

To view the complete overarching roadmap, visit the official [IW-Mission-Control](https://github.com/iwcyberops/IW-Mission-Control) repository.

<br>

---
*Generated & Curated by **IW Cyber Ops** | High-Assurance Cyber Operations & Research*
