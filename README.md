# security-research-for-beginners
A beginner-friendly guide to security research, penetration testing,injection attacks, and vulnerability hunting — with frameworks,examples, and free resources. Zero experience required.






# Security Research for Beginners

> A zero-experience guide to security research, penetration testing,
> injection attacks, and vulnerability hunting. Written in plain English.
> Free. Open source. Beginner-first.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Beginner Friendly](https://img.shields.io/badge/level-beginner-green)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)]()

## What Is This?

This is a **free, beginner-friendly handbook** for anyone who wants to learn
**security research**, **penetration testing**, **bug bounty hunting**, or
**ethical hacking** — even if you have **zero experience** with computers
or programming.

Every guide is written in **plain English**. Every concept is explained
with examples. No jargon without a definition.

## Who Is This For?

- **Complete beginners** who have never touched security before
- **Students** who want a roadmap
- **Developers** who want to understand how their code gets attacked
- **Career switchers** entering cybersecurity
- **Self-taught learners** who are tired of scattered tutorials

## What You Will Learn

| Area | What you will know by the end |
|---|---|
| **Mindset** | How security researchers think — the "assumption audit" |
| **Foundations** | How computers, the web, and HTTP actually work |
| **Tools** | Burp Suite, Browser DevTools, Linux terminal, wordlists |
| **Framework** | The 5-question audit, decision tree, matching matrix |
| **Injections** | Command, SQL, XSS, SSRF, SSTI, XXE, deserialization, path traversal, zip-slip, prompt injection, PDF injection |
| **Misconfigurations** | PATH hijack, dotenv leaks, default-permissive settings |
| **Libraries** | Dangerous vs safe function pairs |
| **Privilege escalation** | Linux privesc, attack chains |
| **AI security** | Embedded browser bugs, prompt injection, AI tool threats |
| **Roadmap** | A 90-day plan to land your first bug |

## Quick Start

New here? Read in this order:

1. [00-start-here/03-the-mindset.md](00-start-here/03-the-mindset.md) — 10 minutes
2. [03-the-framework/README.md](03-the-framework/README.md) — the core method
3. [04-injection-guides/01-command-injection.md](04-injection-guides/01-command-injection.md) — first real attack
4. [10-roadmap/90-day-plan.md](10-roadmap/90-day-plan.md) — your learning plan

## The Core Idea (Read This First)

> **Find the interpreter. Learn its language. Match the payload.
> Prove it with the differential test.**

That's the entire field of vulnerability research, compressed into one
sentence. Every guide in this repo expands on it.

## How Each Guide Is Structured

Every injection guide follows the same format so you always know what to look for:

1. **What it is** — in one paragraph, plain English
2. **The interpreter** — which part of the system processes the input
3. **The payload language** — what the attack looks like
4. **Vulnerable code example** — with the flaw marked
5. **How the attack works** — step by step
6. **The fix** — with fixed code
7. **Bypass techniques** — the full family of tricks
8. **How to test** — the differential test
9. **Real-world examples** — CVEs and case studies

## Table of Contents

- [00 — Start Here](00-start-here/)
- [01 — Foundations](01-foundations/)
- [02 — Tools Setup](02-tools-setup/)
- [03 — The Framework](03-the-framework/) ⭐ **start here after foundations**
- [04 — Injection Guides](04-injection-guides/)
- [05 — Misconfigurations](05-misconfigurations/)
- [06 — Libraries](06-libraries/)
- [07 — Privilege Escalation](07-privilege-escalation/)
- [08 — AI Assistant Security](08-ai-assistant-security/)
- [09 — Resources](09-resources/)
- [10 — Roadmap](10-roadmap/)
- [11 — Glossary](11-glossary/)

## Ethics (Read Before Anything Else)

This repo is for **legal, ethical security research only**.

- Only test systems **you own** or have **written permission** to test.
- Use **legal lab environments** (try [PortSwigger Web Security Academy](https://portswigger.net/web-security), [HackTheBox](https://www.hackthebox.com/), [TryHackMe](https://tryhackme.com/)).
- **Never** attack systems you don't own — it's a crime in every country.
- Read: [00-start-here/02-ethics-and-legal.md](00-start-here/02-ethics-and-legal.md)

## Contributing

Found a typo? Want to add a guide? PRs are welcome.
See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT — free to use, share, and learn from.

## Keywords

security research for beginners, learn penetration testing, ethical hacking
tutorial, bug bounty beginner guide, injection attacks explained,
command injection, sql injection, xss tutorial, ssrf guide, path traversal,
prompt injection, ai security, cybersecurity roadmap, learn hacking,
web security academy, ctf beginner, free security course, infosec handbook