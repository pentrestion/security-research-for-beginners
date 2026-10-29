# The Framework: How to Know If Something Is Vulnerable

This is the heart of the repo. Read it twice.

## The One Sentence

> **Find the interpreter. Learn its language. Match the payload.
> Prove it with the differential test.**

Every vulnerability in this repo follows this pattern.

## What Is an Interpreter?

An **interpreter** is anything that reads a value and does something
based on what that value means.

Examples:
- A **shell** (`bash`) reads a string and runs it as a command.
- A **database** (`MySQL`) reads a query and runs it.
- A **browser** reads HTML and draws a page.
- A **filesystem** reads a path and opens a file.

If your input reaches an interpreter, you can control what it does.
If it doesn't, you can't.

## The 5 Questions (Stage 3 of the framework)

For every input in an app, ask:

1. **Does the code check where the input came from?**
   If no → any page can call it. *Confused deputy bug.*

2. **Does the code check the input AFTER making it normal?**
   If it checks before decoding → `%2e%2e` bypasses `..` filters.

3. **Does the check apply to EVERY place the input can be used?**
   If only the top page is checked → a Worker or iframe escapes.

4. **Does an empty or malformed input mean "allow" or "block"?**
   If empty = allow → default-permissive bug.

5. **Is the checked value self-reported by the caller?**
   If yes → the caller can lie. *Spoofing bug.*

## The Decision Tree
Read the check.
│
├─ No check at all?              → VULNERABLE
├─ Only shape (typeof, regex)?   → VULNERABLE (spoof)
├─ Before normalization?         → VULNERABLE (encoding)
├─ Only one context?             → VULNERABLE (escape)
├─ Empty = allow?                → VULNERABLE (fail-open)
├─ Trusts caller's own claim?    → VULNERABLE (forge)
└─ Compares exact value from
exact trusted source?          → SAFE


## The Prediction Loop

Before you run anything:

1. Name the **exact check** in one sentence.
2. Find the **smallest input** that passes it but reaches the sink.
3. Check **order** — does normalization happen before or after?
4. Check **reachability** — is the sink in the same context?
5. Check **escalation** — does the sink cross a trust zone?

If any step fails, the bypass will not work. Move on.

## The Differential Test

The only proof that counts:

```

Run 1: vulnerable code + payload → does the sink fire?
Run 2: patched code  + payload → does the sink fire?

Vulnerable = Run 1 fires AND Run 2 does not.

```

Anything else is a false positive.

## Why Beginners Miss Bugs

They look for "mistakes." **Researchers look for assumptions.**

Every vulnerable line says, in effect: *"the caller is honest."*
Your job is to ask: **"What if they aren't?"**


Continue to:
- [01-five-questions.md](01-five-questions.md)
- [02-decision-tree.md](02-decision-tree.md)
- [03-matching-matrix.md](03-matching-matrix.md)
- [04-prediction-loop.md](04-prediction-loop.md)
- [05-differential-test.md](05-differential-test.md)
```

---

04-injection-guides/01-command-injection.md — The Template (use for all guides)

```markdown
# Command Injection

**Difficulty:** ⭐ Beginner
**Prerequisites:** [Linux basics](../01-foundations/04-linux-basics.md)

## What It Is (Plain English)

Command injection happens when an app takes your input and passes it to
the **operating system's shell** (like `bash` or `sh`). The shell reads
your input as if it were a command typed in a terminal.

If you can sneak `; id` into the input, the shell runs `id` too.

## The Interpreter

**The shell.** Specifically `/bin/sh`, `/bin/bash`, or `/bin/cmd.exe`.

You know you're facing a shell when you see any of:
- Python: `os.system(...)` or `subprocess.run(..., shell=True)`
- Node: `child_process.exec(...)` or `require('child_process').execSync`
- PHP: `shell_exec(...)`, `system(...)`, `exec(...)`, `passthru(...)`
- Ruby: backticks `` `command` `` or `system(...)`

## The Payload Language

The shell has a grammar. These characters separate commands:

| Payload | What it does |
|---|---|
| `; id` | Run `id` after the original command |
| `&& id` | Run `id` if the first succeeds |
| `\| id` | Pipe output to `id` |
| `\|\| id` | Run `id` if the first fails |
| `` `id` `` | Run `id` and substitute its output |
| `$(id)` | Same as backticks |
| `%0a id` | Newline (URL-encoded) |

## Vulnerable Code

```python
# FLAW: user input goes straight into a shell string
def ping_host(user_input):
    return os.system("ping -c 1 " + user_input)
```

How the Attack Works

Step 1. Attacker sends 127.0.0.1; id
Step 2. The app builds: ping -c 1 127.0.0.1; id
Step 3. The shell runs two commands: ping and id
Step 4. Attacker sees the output of id and knows the attack worked.

The Fix

```python
# FIXED: pass a list, never a string to a shell
import subprocess

def ping_host(user_input):
    return subprocess.run(["ping", "-c", "1", user_input],
                          shell=False, capture_output=True)
```

shell=False (the default) means the input is an argument, not a command.

Bypass Techniques (when shell=True is used but a filter exists)

If the app blocks ; and |, try:

· Newline: %0a id
· Substitution: $(id) or  `id` 
· AND/OR: && id, || id
· Encoding: %3B (URL-encoded ;), %24%28 (URL-encoded $()
· Concatenation: a=id;$a
· Space bypass: {cat,/etc/passwd}, cat$IFS/etc/passwd

How to Test (Differential Test)

```
Run 1: send "127.0.0.1; id"      → do you see uid=...?
Run 2: same on patched code       → do you see uid=...?

If Run 1 shows output and Run 2 doesn't → CONFIRMED.
```

Real-World Examples

· CVE-2021-44228 (Log4Shell) — indirectly reached a shell in many apps
· CVE-2024-3400 (PAN-OS) — command injection in GlobalProtect
· Many IoT router CVEs — ping diagnostics always vulnerable

Practice Labs (Legal)

· PortSwigger: OS Command Injection
· TryHackMe: Command Injection

Next Guide

→ 02-argument-injection.md — when shell=False isn't enough

```