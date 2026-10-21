# 01 · Scoping and rules of engagement (labs 2.2.9 and 2.2.10)

**Goal:** before touching anything, write the document that says what may be tested, how, and who signs off.

I wrote a scope and rules-of-engagement document for a test of a small South African business's public website and application form. The full document stays private because it names a live server. These are the decisions in it:

- **Legal footing.** POPIA (Act 4 of 2013) requires "appropriate, reasonable" safeguards for personal information and that risks are regularly verified. A penetration test is one way to provide that evidence, and the document says so without claiming the Act requires one. Section 2 of the Cybercrimes Act (Act 19 of 2020) makes unlawful access to a computer system a crime, so a signed scope is the evidence that the client consented. Nothing starts before sign-off.
- **The tightest possible target.** Public DNS and BGP data showed the site sits on a **shared hosting IP** that also serves many unrelated domains. So the scope authorises that single address (`/32`) and the named URLs only. Scanning the surrounding range would mean testing other people's servers.
- **Explicitly out of scope:** third-party platforms (analytics, CRM, automation and AI providers), client and partner systems, payroll systems, physical attacks, phishing and social engineering, denial-of-service, and bulk data exfiltration or destruction.
- **Testing window:** Monday to Friday, 18:00–23:00 SAST, and only with written approval to go outside it.
- **Data handling:** if the test exposes real personal information, the tester stops touching that record, documents only the minimum needed to prove the finding, keeps no copy, and waits for direction from the client.
- **Stop condition:** if an in-scope system becomes unstable or unavailable, testing stops at once and the emergency contact is called. The site publishes no phone number, so one must be supplied before testing begins.
- **Reporting:** each finding gives the asset, evidence, business impact, severity and fix, with evidence kept free of personal data, credentials and secrets.

**What I learned:** the hardest scoping call was the shared IP. The obvious "scan the server" instruction would have dragged in systems nobody had authorised.
