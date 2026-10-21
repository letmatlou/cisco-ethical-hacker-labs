# Cisco Ethical Hacker labs

My write-ups for the Cisco Networking Academy **Ethical Hacker** course, which I'm working through alongside my BSc in Security and Network Engineering. Each write-up covers what I ran, what I found, why it matters and how I'd fix it.

> **Scope and ethics.** Every scan, capture and lookup here was run against my own lab machines on a private VirtualBox network: a Kali Linux attacker (`10.10.10.11`) and a deliberately vulnerable Metasploitable 2 target (`10.10.10.10`). Nothing here was pointed at a system I don't own or have written permission to test.

## Lab environment

| Role | System | Address |
|---|---|---|
| Attacker | Kali Linux 2026.2 (VirtualBox) | 10.10.10.11 |
| Target | Metasploitable 2 (VirtualBox) | 10.10.10.10 |

## Write-ups

| # | Lab | Course ref | Tools | What it shows |
|---|---|---|---|---|
| 01 | [Scoping and rules of engagement](labs/01-scoping-and-rules-of-engagement/) | 2.2.9, 2.2.10 | — | Writing a test scope under POPIA and the Cybercrimes Act |
| 02 | [Enumeration with Nmap](labs/02-nmap-enumeration/) | 3.2.6 | Nmap | 23 open services found and fingerprinted in 12 seconds |
| 03 | [Network sniffing with Wireshark](labs/03-wireshark-sniffing/) | 3.2.10 | Wireshark, tcpdump | Reading a Telnet username and password straight off the wire |
| 04 | [Vulnerability research](labs/04-vulnerability-research/) | 3.3.6, 3.4.3 | Bash, jq, NVD API | Matching scanned versions to known CVEs with a small lookup script |

Done, write-ups still to come: OSINT tools (3.1.4) and packet crafting with Scapy (3.2.9).

## What I'm taking from these labs
- **Old, cleartext services are the cheapest way in.** Telnet, FTP and the r-services hand over credentials to anyone on the path.
- **Version numbers are evidence.** A banner like `vsftpd 2.3.4` maps straight to a published CVE, so fingerprinting is half the attack.
- **Scope comes first.** The most useful thing I wrote in module 2 wasn't an exploit. It was a document saying exactly what I'm allowed to touch.
