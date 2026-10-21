# 02 · Enumeration with Nmap (lab 3.2.6)

**Goal:** find every listening service on the target and identify its software and version.

```bash
sudo nmap -sV -v -oN recon-test.txt 10.10.10.10
```
- `-sV` probes each open port to fingerprint the service and version.
- `-oN` saves normal output to a file, kept here as [`scan.txt`](scan.txt).
- Running as root gives Nmap a SYN ("half-open") scan by default, which is faster and quieter than a full TCP connect.

## Result
**23 open TCP ports in 11.5 seconds** (977 closed). Highlights:

| Port | Service | Why it stands out |
|---|---|---|
| 21 | vsftpd **2.3.4** | A release of this version was shipped with a backdoor (see lab 04) |
| 23 | Linux telnetd | Logins cross the network in cleartext (proved in lab 03) |
| 512–514 | rexec, rlogin, rsh | 1990s remote-shell services with host-based trust, no encryption |
| 1524 | **bindshell** | Nmap reports a root shell listening with no authentication at all |
| 3306, 5432 | MySQL 5.0, PostgreSQL 8.3 | Databases exposed directly to the network |
| 5900 | VNC 3.3 | Remote desktop on an old protocol version |
| 6667 | UnrealIRCd | A version of this was shipped with a backdoor (see lab 04) |
| 139, 445 | Samba 3.x | Old SMB, with known remote code execution flaws in that range |

## If this were a real server
1. Turn off what isn't needed: Telnet, the r-services, the bindshell, VNC and IRC have no business on a server.
2. Put databases behind a firewall rule so only the application host can reach them.
3. Replace Telnet and FTP with SSH and SFTP.
4. Patch or replace every service whose version matches a known CVE.

**What I learned:** `-sV` turns "port 21 is open" into "vsftpd 2.3.4 is running", and the second is what an attacker searches for.
