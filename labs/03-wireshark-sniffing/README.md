# 03 · Network sniffing with Wireshark (lab 3.2.10)

**Goal:** show why cleartext protocols are dangerous by capturing a login and reading it back.

I captured traffic while logging in to the target over Telnet (port 23) from Kali, then saved it as [`telnet-session.pcap`](telnet-session.pcap). It holds 155 packets over a few seconds.

## Reading it
In Wireshark: **Analyze → Follow → TCP Stream** on the port 23 conversation. The same thing from the command line:
```bash
tcpdump -nn -A -r telnet-session.pcap 'tcp port 23'
```

What the capture shows, in order:
1. The TCP three-way handshake (SYN, SYN-ACK, ACK) from `10.10.10.11` to `10.10.10.10:23`.
2. Telnet option negotiation, which even leaks the client's terminal type (`XTERM-256COLOR`) and display name.
3. The Metasploitable login banner, sent in plain text.
4. **The username and password, typed one character per packet and readable in full:** `msfadmin` / `msfadmin`. Every keystroke is its own TCP segment, and the server echoes it back.
5. A shell prompt (`msfadmin@metasploitable:~$`) and a `ping` command run on the target, with the ICMP traffic it generated.

(These are Metasploitable's public default credentials, so nothing secret is exposed by publishing this file.)

## Why it matters
Anyone on the network path (a shared Wi-Fi, a compromised switch, an ARP-spoofing attacker) sees exactly what I saw. Encryption is the fix, not a stronger password: a strong password sent over Telnet is captured just as easily.

## Fix
Disable Telnet and use SSH. Where an old device only speaks Telnet, isolate it on a management VLAN that ordinary users can't reach.

**What I learned:** seeing a password come through one character per packet made "cleartext" concrete in a way the textbook definition didn't.
