<!-- 
SEO METADATA & KEYWORDS (Invisible to readers, visible to Google Crawlers)
Keywords: IW Cyber Ops, Muhammad Imran Wakeel, OverTheWire Leviathan Solutions, Leviathan Wargame Walkthrough, Linux Privilege Escalation, ltrace Dynamic Tracing, strace System Calls, SUID Binary Exploitation, Symlink Attacks, Command Injection in C, access vs system, Reverse Engineering Wargames, Cybersecurity Knowledge Base.
-->

# 🐉 OverTheWire Leviathan — Complete Tactical Walkthrough

> **Platform:** OverTheWire Wargames (`leviathan`)  
> **Target Host:** `leviathan.labs.overthewire.org` (Port: `2223`)  
> **System Operator & Lead Researcher:** Muhammad Imran Wakeel (`@iwcyberops`)  
> **Mission Scope:** Deconstruct Linux binary logic flaws, dynamic library call interception, file descriptor redirection, and local privilege escalation.

---

## 🧭 Operational Overview

The **Leviathan** wargame marks the critical transition from pure Linux command-line administration into **Binary Logic Auditing and Local Privilege Escalation (LPE).**

Unlike standard file-hunting exercises, Leviathan presents custom compiled SUID executables running with elevated user privileges. To capture the next level credentials stored inside `/etc/leviathan_pass/`, an operator must inspect binaries without source code, trace dynamic library calls (**`ltrace`**), intercept system calls (**`strace`**), bypass filename validation checks, weaponize symbolic links (**`ln -s`**), and decode raw bitstreams directly inside the terminal.

---
