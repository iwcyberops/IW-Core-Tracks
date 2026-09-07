<!-- =========================================================================
   PROJECT: IW Cyber Ops — Arsenal Vault (Offensive Operations & War Games)
   AUTHOR: Muhammad Imran | IW Cyber Ops (@iwcyberops)
   TRACK: Linux Systems Exploitation & Tactical Wargame Methodology
   MODULE: OverTheWire — Bandit Complete Operational Breakdown (Level 00 to 33)
   DOCUMENT: 01-bandit-methodology.md
   NOTE: In compliance with OverTheWire guidelines, raw flags are REDACTED.
   ========================================================================= -->

# ⚔️ OverTheWire: Bandit — Complete Tactical Operations Manual

> **IW Cyber Ops Arsenal | Offensive Operations & Systems Research**  
> *Author: Muhammad Imran (@iwcyberops)*  
> *Target: bandit.labs.overthewire.org | Port: 2220*  
> *Classification: Operator Field Manual & Methodological Reference (Flags Redacted)*

---

## 📑 Operational Table of Contents

* [Level 00 ──> 01: Initial SSH Ingress](#level-00----01-initial-ssh-ingress)
* [Level 01 ──> 02: Standard Dashed Files & Option Escaping](#level-01----02-standard-dashed-files--option-escaping)
* [Level 02 ──> 03: Whitespace & Shell Metacharacter Escaping](#level-02----03-whitespace--shell-metacharacter-escaping)
* [Level 03 ──> 04: Hidden Inode Identification](#level-03----04-hidden-inode-identification)
* [Level 04 ──> 05: Multi-File ASCII & Binary Disambiguation](#level-04----05-multi-file-ascii--binary-disambiguation)
* [Level 05 ──> 06: Deep Filesystem Query by Specific Attributes](#level-05----06-deep-filesystem-query-by-specific-attributes)
* [Level 06 ──> 07: Global Root Hierarchy User/Group Hunting](#level-06----07-global-root-hierarchy-usergroup-hunting)
* [Level 07 ──> 08: Pattern Extraction via Regular Expressions](#level-07----08-pattern-extraction-via-regular-expressions)
* [Level 08 ──> 09: Frequency Analysis & Duplicate Elimination](#level-08----09-frequency-analysis--duplicate-elimination)
* [Level 09 ──> 10: Binary Scraping & Delimited Text Recovery](#level-09----10-binary-scraping--delimited-text-recovery)
* [Level 10 ──> 11: Base64 Decoding Pipeline](#level-10----11-base64-decoding-pipeline)
* [Level 11 ──> 12: Symmetric Caesar/ROT13 De-obfuscation](#level-11----12-symmetric-caesarrot13-de-obfuscation)
* [Level 12 ──> 13: Multi-Layer Compression Reversal (Hex to Tar/Gz/Bz2)](#level-12----13-multi-layer-compression-reversal-hex-to-targbz2)
* [Level 13 ──> 14: Asymmetric Cryptographic Authentication (SSH Key Pivot)](#level-13----14-asymmetric-cryptographic-authentication-ssh-key-pivot)
* [Level 14 ──> 15: Raw TCP Socket Interfacing](#level-14----15-raw-tcp-socket-interfacing)
* [Level 15 ──> 16: Encrypted SSL/TLS Client Handshake](#level-15----16-encrypted-ssltls-client-handshake)
* [Level 16 ──> 17: Tactical Port Scanning & Multi-Port TLS Recon](#level-16----17-tactical-port-scanning--multi-port-tls-recon)
* [Level 17 ──> 18: File Differential Analysis & Delta Identification](#level-17----18-file-differential-analysis--delta-identification)
* [Level 18 ──> 19: Non-Interactive Shell Invocation (RC Trap Bypass)](#level-18----19-non-interactive-shell-invocation-rc-trap-bypass)
* [Level 19 ──> 20: SUID Binary Execution Proxying](#level-19----20-suid-binary-execution-proxying)
* [Level 20 ──> 21: Multi-Terminal IPC Client-Server Handshake](#level-20----21-multi-terminal-ipc-client-server-handshake)
* [Level 21 ──> 22: Cron Execution Path & Temp Extraction](#level-21----22-cron-execution-path--temp-extraction)
* [Level 22 ──> 23: Reverse Engineering Shell Variables & MD5 Namespaces](#level-22----23-reverse-engineering-shell-variables--md5-namespaces)
* [Level 23 ──> 24: Time-Scheduled Shell Script Poisoning / Staging](#level-23----24-time-scheduled-shell-script-poisoning--staging)
* [Level 24 ──> 25: Automated Network Daemon PIN Brute-Forcing](#level-24----25-automated-network-daemon-pin-brute-forcing)
* [Level 25 ──> 26: Restricted Terminal Breakout (Pager Escape Mechanics)](#level-25----26-restricted-terminal-breakout-pager-escape-mechanics)
* [Level 26 ──> 27: SUID Privilege Escalation Execution](#level-26----27-suid-privilege-escalation-execution)
* [Level 27 ──> 28: Git Clone over Custom Non-Standard SSH Port](#level-27----28-git-clone-over-custom-non-standard-ssh-port)
* [Level 28 ──> 29: Git Commit Log Auditing & Historical Diffing](#level-28----29-git-commit-log-auditing--historical-diffing)
* [Level 29 ──> 30: Multi-Branch Exploration & Unmerged Trees](#level-29----30-multi-branch-exploration--unmerged-trees)
* [Level 30 ──> 31: Tagged Commit Analysis & Release Scrape](#level-30----31-tagged-commit-analysis--release-scrape)
* [Level 31 ──> 32: Overriding Gitignore Directives & Remote Pushing](#level-31----32-overriding-gitignore-directives--remote-pushing)
* [Level 32 ──> 33: Uppercase Restricted Shell Escape via `$0`](#level-32----33-uppercase-restricted-shell-escape-via-0)

---

## Level 00 ──> 01: Initial SSH Ingress

* **Objective:** Establish the initial secure shell connection to the remote server on non-standard port 2220.
* **Tactical Logic:** Standard SSH uses port 22. Target requires explicit port targeting (`-p 2220`).

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
# Input Password: bandit0
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT1_PASSWORD]
```

---

## Level 01 ──> 02: Standard Dashed Files & Option Escaping

* **Objective:** Read the contents of a file named `-` situated in the root of the user's home directory.
* **Tactical Logic:** Commands like `cat -` interpret `-` as standard input (`stdin`) or an invalid flag argument. The shell parser must be instructed to treat `-` as a literal relative filesystem path (`./-`) or use the POSIX end-of-command-options delimiter `--`.

```bash
# Vector A: Relative Path Resolution
cat ./-

# Vector B: Stream Redirection
cat < -

# Vector C: POSIX Argument Terminator
cat -- -
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT2_PASSWORD]
```

---

## Level 02 ──> 03: Whitespace & Shell Metacharacter Escaping

* **Objective:** Access the contents of a file with arbitrary spaces in the name: `--spaces in this filename--`.
* **Tactical Logic:** The bash word splitter uses spaces as token delimiters. The filename must be encapsulated in string quotes or escaped with backslashes (`\`) to preserve literal whitespace.

```bash
# Execution Vector:
cat "./--spaces in this filename--"
# Alternative:
cat --spaces\ in\ this\ filename--
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT3_PASSWORD]
```

---

## Level 03 ──> 04: Hidden Inode Identification

* **Objective:** Retrieve password stored inside a hidden file inside the `inhere` directory.
* **Tactical Logic:** In Linux, files beginning with a period `.` are excluded from default directory listings. The `-a` (all) flag exposes hidden entries.

```bash
cd inhere
ls -la
cat ./...Hiding-From-You
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT4_PASSWORD]
```

---

## Level 04 ──> 05: Multi-File ASCII & Binary Disambiguation

* **Objective:** Locate the only human-readable ASCII text file among multiple pseudo-flag binary files prefixed with `-file0*` inside `inhere`.
* **Tactical Logic:** Instead of manually reading every binary file, `file ./*` inspects the magic bytes of every file in the directory to identify ASCII text.

```bash
cd inhere
# Inspect MIME / Magic signatures
file ./*
# Direct extraction based on signature:
cat ./-file07
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT5_PASSWORD]
```

---

## Level 05 ──> 06: Deep Filesystem Query by Specific Attributes

* **Objective:** Locate a file under `inhere` matching three specific constraints:
  1. Human-readable text
  2. Exactly 1033 bytes in size
  3. Non-executable permissions
* **Tactical Logic:** Use the `find` engine with precise attribute constraints: `-size 1033c` (exact bytes) and `! -perm /111` (not executable).

```bash
find inhere/ -type f -size 1033c ! -perm /111 -exec cat {} +
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT6_PASSWORD]
```

---

## Level 06 ──> 07: Global Root Hierarchy User/Group Hunting

* **Objective:** Find a file on the entire system owned by user `bandit7`, group `bandit6`, and sized exactly 33 bytes.
* **Tactical Logic:** Searching from the root directory (`/`) produces hundreds of `Permission denied` errors. Redirecting `stderr` (FD 2) to `/dev/null` silences permission errors, isolating the exact matching path.

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null -exec cat {} +
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT7_PASSWORD]
```

---

## Level 07 ──> 08: Pattern Extraction via Regular Expressions

* **Objective:** Extract the password positioned directly next to the word `millionth` inside a massive line-heavy file `data.txt`.
* **Tactical Logic:** Reading the entire file via `cat` or `less` wastes operational time. `grep` parses the data stream and extracts only the relevant matching string.

```bash
grep "millionth" data.txt | awk '{print $2}'
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT8_PASSWORD]
```

---

## Level 08 ──> 09: Frequency Analysis & Duplicate Elimination

* **Objective:** Extract the only string in `data.txt` that occurs exactly once among hundreds of duplicate lines.
* **Tactical Logic:** The `uniq` utility only compares adjacent identical lines. The data stream must first pass through `sort`, then into `uniq -u` (unique only) or `uniq -c` (count frequency).

```bash
sort data.txt | uniq -u
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT9_PASSWORD]
```

---

## Level 09 ──> 10: Binary Scraping & Delimited Text Recovery

* **Objective:** Extract human-readable password from binary garbage in `data.txt`, preceded by multiple `=` characters.
* **Tactical Logic:** `strings` scans binary memory dumps or data blobs for sequences of 4 or more printable ASCII characters. Filtering with `grep` extracts the delimited password.

```bash
strings data.txt | grep "===" | tail -n 1 | awk -F '=' '{print $NF}' | tr -d ' '
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT10_PASSWORD]
```

---

## Level 10 ──> 11: Base64 Decoding Pipeline

* **Objective:** Decode Base64 encoded payload inside `data.txt`.
* **Tactical Logic:** Direct pipe to system standard `base64` utility with the decode (`-d`) flag.

```bash
base64 -d data.txt
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT11_PASSWORD]
```

---

## Level 11 ──> 12: Symmetric Caesar/ROT13 De-obfuscation

* **Objective:** Decode standard ROT13 cipher where every alphabetical character is shifted by 13 positions.
* **Tactical Logic:** The `tr` (translate) utility maps the lower and uppercase alphabets across a 13-character offset interval `[A-Za-z]` → `[N-ZA-Mn-za-m]`.

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT12_PASSWORD]
```

---

## Level 12 ──> 13: Multi-Layer Compression Reversal (Hex to Tar/Gz/Bz2)

* **Objective:** Reverse an iterative compressed hex dump into its original plaintext file.
* **Tactical Logic:**
  1. Restore ASCII hex dump to pure binary via `xxd -r`.
  2. Inspect format using `file`.
  3. Decompress sequentially using appropriate algorithms (`gunzip`, `bunzip2`, `tar`, `unxz`).

```bash
# 1. Setup isolated operational workspace in /tmp
mkdir /tmp/iw_vault && cd /tmp/iw_vault
cp ~/data.txt .

# 2. Reverse Hex Dump
xxd -r data.txt payload.bin

# 3. Iterative Signature Probing & Extraction Loop
file payload.bin                     # Output: gzip compressed data
mv payload.bin data.gz && gunzip data.gz

file data                            # Output: bzip2 compressed data
mv data data.bz2 && bunzip2 data.bz2

file data                            # Output: POSIX tar archive
tar -xvf data                        # Extracts: data5.bin

file data5.bin                       # Output: POSIX tar archive
tar -xvf data5.bin                   # Extracts: data6.bin

file data6.bin                       # Output: bzip2 compressed data
mv data6.bin data6.bz2 && bunzip2 data6.bz2

file data6                           # Output: POSIX tar archive
tar -xvf data6                       # Extracts: data8.bin

file data8.bin                       # Output: gzip compressed data
mv data8.bin data8.gz && gunzip data8.gz

# 4. Final Payload Extraction
cat data8
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT13_PASSWORD]
```

---

## Level 13 ──> 14: Asymmetric Cryptographic Authentication (SSH Key Pivot)

* **Objective:** Pivot to `bandit14` using a private RSA key `sshkey.private` stored in the home directory.
* **Tactical Logic:** SSH allows authenticating via public/private key pairs using the `-i` (identity file) flag instead of a password.

```bash
ssh -i sshkey.private -p 2220 bandit14@bandit.labs.overthewire.org
```

* **Password Retrieval for bandit14:**
```bash
cat /etc/bandit_pass/bandit14
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT14_PASSWORD]
```

---

## Level 14 ──> 15: Raw TCP Socket Interfacing

* **Objective:** Submit current level's password to an active TCP socket running on `localhost:30000` to receive the next password.
* **Tactical Logic:** Utilize `nc` (Netcat) to establish a raw transport layer stream and pipe the password.

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT15_PASSWORD]
```

---

## Level 15 ──> 16: Encrypted SSL/TLS Client Handshake

* **Objective:** Submit current password to an encrypted TLS service running on `localhost:30001`.
* **Tactical Logic:** Standard Netcat fails over TLS/SSL streams. Use `openssl s_client` with `-quiet` to establish an encrypted handshake and suppress diagnostic certificates.

```bash
openssl s_client -connect localhost:30001 -quiet
# Transmit bandit15 password via the TLS stream
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT16_PASSWORD]
```

---

## Level 16 ──> 17: Tactical Port Scanning & Multi-Port TLS Recon

* **Objective:** Scan ports in range `31000-32000`, identify the only listening service speaking TLS and returning credentials.
* **Tactical Logic:**
  1. Scan listening TCP ports with `nmap`.
  2. Test each open port with `openssl s_client`.
  3. Capture the returned RSA private key.

```bash
# 1. Port Identification
nmap -sV -p 31000-32000 localhost

# 2. Transmit credentials to TLS service on Port 31790
echo "<BANDIT_16_PASSWORD>" | openssl s_client -connect localhost:31790 -quiet > /tmp/bandit17.key

# 3. Secure Key Permissions & Connect
chmod 600 /tmp/bandit17.key
ssh -i /tmp/bandit17.key -p 2220 bandit17@bandit.labs.overthewire.org
```

---

## Level 17 ──> 18: File Differential Analysis & Delta Identification

* **Objective:** Compare `passwords.old` and `passwords.new` to locate the single altered line.
* **Tactical Logic:** The `diff` utility computes the minimal delta between two line files.

```bash
diff passwords.old passwords.new | grep ">" | awk '{print $2}'
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT18_PASSWORD]
```

---

## Level 18 ──> 19: Non-Interactive Shell Invocation (RC Trap Bypass)

* **Objective:** Log into `bandit18` where `.bashrc` terminates interactive sessions upon connection (`logout`).
* **Tactical Logic:** Appending a command at the end of an SSH string bypasses the allocation of an interactive login shell and `.bashrc` execution, running the binary directly.

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 'cat readme'
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT19_PASSWORD]
```

---

## Level 19 ──> 20: SUID Binary Execution Proxying

* **Objective:** Read `/etc/bandit_pass/bandit20` using an SUID executable `./bandit20-do`.
* **Tactical Logic:** An executable with the Set-UID (`s`) bit runs with the effective permissions of its file owner (`bandit20`). Passing `cat` as an argument executes it with elevated privileges.

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT20_PASSWORD]
```

---

## Level 20 ──> 21: Multi-Terminal IPC Client-Server Handshake

* **Objective:** Use an SUID binary `./suconnect` that connects to a local network port, validates the current level password, and returns the next level password.
* **Tactical Logic:**
  1. Spawn a Netcat listener in the background sending the current password.
  2. Invoke `./suconnect` pointing to the listener port.

```bash
# Terminal 1 / Background Process:
echo "<BANDIT_20_PASSWORD>" | nc -lvnp 8080 &

# Terminal 2 / Foreground Invocation:
./suconnect 8080
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT21_PASSWORD]
```

---

## Level 21 ──> 22: Cron Execution Path & Temp Extraction

* **Objective:** Inspect scheduled cron jobs running under system daemon to recover target password.
* **Tactical Logic:** Examine `/etc/cron.d/`, inspect the shell script executed by user `bandit22`, and read the dynamic destination file in `/tmp`.

```bash
# 1. Audit Cron Jobs
cat /etc/cron.d/cronjob_bandit22

# 2. Inspect Target Script
cat /usr/bin/cronjob_bandit22.sh

# 3. Read Staged Password
cat /tmp/<DYNAMIC_TEMP_PATH>
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT22_PASSWORD]
```

---

## Level 22 ──> 23: Reverse Engineering Shell Variables & MD5 Namespaces

* **Objective:** Reverse engineer the target file generation algorithm executed by `bandit23`'s cron job.
* **Tactical Logic:** The script hashes a string containing the username via `md5sum`. Replicate the hash generation locally for user `bandit23` to calculate the exact file path.

```bash
# 1. Inspect Cron Logic
cat /usr/bin/cronjob_bandit23.sh

# 2. Calculate dynamic hash for bandit23
mytarget=$(echo I am user bandit23 | md5sum | cut -d ' ' -f 1)

# 3. Extract target file
cat /tmp/$mytarget
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT23_PASSWORD]
```

---

## Level 23 ──> 24: Time-Scheduled Shell Script Poisoning / Staging

* **Objective:** Exploit a cron job executing all user scripts dropped into `/var/spool/bandit24/foo/` with `bandit24` privileges.
* **Tactical Logic:** Write a bash script that copies `/etc/bandit_pass/bandit24` to a world-writable path in `/tmp`, grant full execution rights (`chmod 777`), and wait for cron to execute it.

```bash
# 1. Build Payload
mkdir /tmp/iw_pwn && cd /tmp/iw_pwn
echo '#!/bin/bash' > exploit.sh
echo 'cat /etc/bandit_pass/bandit24 > /tmp/iw_pwn/flag.txt' >> exploit.sh
echo 'chmod 666 /tmp/iw_pwn/flag.txt' >> exploit.sh

# 2. Set World-Writable Permissions
chmod 777 exploit.sh

# 3. Deploy to Cron Spool Directory
cp exploit.sh /var/spool/bandit24/foo/

# 4. Wait 60 seconds & Extract
cat /tmp/iw_pwn/flag.txt
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT24_PASSWORD]
```

---

## Level 24 ──> 25: Automated Network Daemon PIN Brute-Forcing

* **Objective:** Brute-force a 4-digit PIN (`0000` to `9999`) against a daemon on `localhost:30002` alongside the `bandit24` password.
* **Tactical Logic:** Bash range brace expansion `{0000..9999}` generates all 10,000 combinations instantly, piped through a single Netcat TCP stream.

```bash
for pin in {0000..9999}; do
    echo "<BANDIT_24_PASSWORD> $pin"
done | nc localhost 30002 | grep -v "Wrong"
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT25_PASSWORD]
```

---

## Level 25 ──> 26: Restricted Terminal Breakout (Pager Escape Mechanics)

* **Objective:** Escape a restricted shell configured with `/usr/bin/showtext` which displays text via `more` and exits immediately.
* **Tactical Logic:**
  1. Shrink the terminal window dimensions vertically.
  2. When SSH connects, `more` pauses output because it cannot fit the text on screen.
  3. Hit `v` inside `more` to spawn `vi` editor.
  4. Break out into a full Bash shell from `vi` using `:set shell=/bin/bash` followed by `:shell`.

```bash
# Inside Vi Command Mode:
:set shell=/bin/bash
:shell

# Once inside interactive shell:
cat /etc/bandit_pass/bandit26
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT26_PASSWORD]
```

---

## Level 26 ──> 27: SUID Privilege Escalation Execution

* **Objective:** Execute `./bandit27-do` SUID binary to extract `bandit27` credentials.
* **Tactical Logic:** Direct command execution proxy identical to Level 19.

```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT27_PASSWORD]
```

---

## Level 27 ──> 28: Git Clone over Custom Non-Standard SSH Port

* **Objective:** Clone a remote Git repository running over an SSH daemon on port 2220.
* **Tactical Logic:** Standard `git clone` defaults to port 22. Target requires specifying the port explicitly in the SSH URL syntax.

```bash
mkdir /tmp/repo_28 && cd /tmp/repo_28
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo

cat repo/README.md
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT28_PASSWORD]
```

---

## Level 28 ──> 29: Git Commit Log Auditing & Historical Diffing

* **Objective:** Extract password removed from a Git repository in previous revisions.
* **Tactical Logic:** Developers frequently commit credentials and remove them in later commits. `git log -p` displays commit history alongside the line-by-line patch delta.

```bash
cd repo/
git log -p -2
# Inspect deletion line marked with '-'
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT29_PASSWORD]
```

---

## Level 29 ──> 30: Multi-Branch Exploration & Unmerged Trees

* **Objective:** Retrieve password stored inside an alternate Git branch.
* **Tactical Logic:** Inspect remote tracking branches using `git branch -a` and checkout the unmerged developmental branch (`dev`).

```bash
cd repo/
git branch -a
git checkout dev
cat README.md
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT30_PASSWORD]
```

---

## Level 30 ──> 31: Tagged Commit Analysis & Release Scrape

* **Objective:** Discover credentials hidden within Git metadata tags.
* **Tactical Logic:** Git tags represent snapshots. `git tag` lists all tags; `git show <tagname>` inspects the specific tagged object.

```bash
cd repo/
git tag
git show secret
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT31_PASSWORD]
```

---

## Level 31 ──> 32: Overriding Gitignore Directives & Remote Pushing

* **Objective:** Push a required file `key.txt` with content `May I come in?` to remote Git repository where `*.txt` is ignored by `.gitignore`.
* **Tactical Logic:** The `-f` (force) flag overrides `.gitignore` rules during `git add`.

```bash
cd repo/
echo "May I come in?" > key.txt
git add -f key.txt
git commit -m "Bypass gitignore"
git push origin master
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT32_PASSWORD]
```

---

## Level 32 ──> 33: Uppercase Restricted Shell Escape via `$0`

* **Objective:** Escape a custom restricted shell that automatically converts all command inputs to uppercase letters.
* **Tactical Logic:** In POSIX shells, `$0` is a special parameter representing the executing binary name of the current shell (e.g., `/bin/sh` or `sh`). Because `$0` contains no letters, the uppercase filter cannot modify it, triggering an unconstrained lowercase subshell.

```bash
# At the >> prompt:
$0

# Once dropped into standard sh/bash:
cat /etc/bandit_pass/bandit33
```

```text
[Flag Status]: RECOVERED
[Next Level Password]: [REDACTED_BANDIT33_PASSWORD]
```

---

<!-- =========================================================================
   [IW CYBER OPS] - INTERNAL RESEARCH USE ONLY
   Repository: https://github.com/iwcyberops/IW-Arsenal
   ========================================================================= -->
