# Phishing & Macro Analysis

Analysing a phishing email that delivered a malicious Office macro, and documenting the attacker's evasion techniques with MITRE ATT&CK. Part of the CYB2100 Cyber Defense exam at Kristiania.

## Overview

The sample was a phishing email carrying a password-protected archive with a weaponised Word document. I worked through how the attack was built to slip past automated defences, then mapped the techniques to the MITRE ATT&CK framework.

## Evasion techniques identified

- **Password-protected archive** – stops automated security systems and sandboxes from inspecting the contents until the user unlocks it manually
- **Social engineering** – the email talks the user into enabling macros and ignoring security warnings
- **VBA macro loader** – hidden code that activates when the document opens and macros are allowed
- **Base64 encoding** – the payload is encoded so antivirus can't read the final code before it's decoded
- **Living off the land** – the macro launches a legitimate system tool (PowerShell) to run the payload, avoiding its own malware binary

## Analysis workflow

1. Decrypted the email and opened the document with the supplied password
2. Inspected the macros with **oletools** to confirm the VBA loader and extract its behaviour
3. Documented the full chain from delivery to execution and mapped it against MITRE ATT&CK

## Defensive measures

The report recommends email authentication (**SPF, DKIM, DMARC**) to make spoofed senders harder, mapped to ATT&CK technique T1566, together with user-awareness training (mitigation M1017) and account-use policies (M1036).

## Tools & concepts

oletools (olevba) · MITRE ATT&CK · VBA / macro reverse engineering · SPF/DKIM/DMARC · phishing analysis

## What I took from it

Seeing how many small, legitimate-looking steps chain together into a working attack changed how I read suspicious emails. Each layer is cheap for the attacker and expensive for the defender if you're only looking at one of them at a time.
