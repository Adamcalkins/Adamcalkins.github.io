---
title: "🐻 Threat Detection Based on Russian APT Group TTPs – A Splunk-Based Lab Project"
date: 2025-07-19 10:31:00 +02:00
categories: [Project]
tags: [APT, MITRE ATT&CK, Splunk, Blue Team]
---

# Blue Team - Project

## 📋 About the Project

Cybersecurity threats from nation-state actors continue to evolve in sophistication, scope, and persistence. Among them, Russian Advanced Persistent Threat (APT) groups have been particularly aggressive and technically advanced in targeting governmental, military, diplomatic, and critical infrastructure entities.

Our project, “**Threat Detection Rules Based on Activities of Cybercriminal Groups Attributed to Russia**”, is a hands-on initiative focused on identifying, testing, and detecting real-world attack techniques mapped to specific APT groups using **MITRE ATT&CK** and **Splunk**.

## 🔍 Objective

The primary goal was to design and validate practical **detection rules** for techniques used by Russian APT groups such as **APT28 (Fancy Bear)**, **APT29 (Cozy Bear)**, **APT44 (Sandworm)**, and **Turla**. Each group’s known Tactics, Techniques, and Procedures (TTPs) were mapped and tested in a simulated environment. The rules were implemented in **Splunk SPL (Search Processing Language)** and validated through scenario-based threat emulation.

## 🛠️ Lab Setup

The project was conducted in a controlled, virtualized lab environment consisting of two virtual machines:

- **Windows 11 (Victim Host)**: Configured with Sysmon for advanced event logging and Atomic Red Team for simulating adversarial behavior.
- **Ubuntu Server (Monitoring Host)**: Deployed with **Splunk Enterprise** to ingest and analyze logs from the Windows host.

This setup allowed us to safely execute malicious behavior and evaluate our detection mechanisms in a realistic, yet fully isolated setting.

## 👾 APT Groups Analyzed

We selected the following APT groups based on their operational history and impact:

- **APT28 (Fancy Bear)** – Known for spearphishing, credential dumping, and use of malware like X-Agent and Zebrocy.
- **APT29 (Cozy Bear)** – Operates stealthily using tools such as SUNBURST, FoggyWeb, and extensive PowerShell scripting.
- **APT44 (Sandworm Team)** – Responsible for destructive attacks including NotPetya and attacks on Ukrainian infrastructure.
- **Turla** – Long-term espionage actor using fileless malware and piggybacking techniques.

We studied their behavior across multiple attack stages: initial access, privilege escalation, persistence, evasion, lateral movement and data exfiltration.

## 🧪 Techniques and Detection Logic

We developed custom SPL detection rules for 16 MITRE ATT&CK techniques, including:

- ``T1140 – Deobfuscate/Decode Files or Information``
- ``T1546.003 – WMI Event Subscription``
- ``T1070.001 – Clear Windows Event Logs``
- ``T1059.001 – PowerShell Execution``
- ``T1560.001 – Archive Collected Data``
- ``T1113 – Screen Capture``
- ``T1053.005 – Scheduled Tasks``
- ``…and more.``

Each rule leverages logs from Sysmon, Windows Security and/or PowerShell Operational logging. We correlated process creation, file writes, script block logging, registry edits, and event channel activity to trigger precise detections.

Each detection was accompanied by a simulated test case using Invoke-Atomic, allowing us to verify alert generation in Splunk and fine-tune rule accuracy.

## 📊 Results

The project successfully demonstrated:

- Effective correlation of log data to detect advanced adversary behavior.
- Practical implementation of MITRE ATT&CK mapping for real-world threats.
- Creation of a modular detection pipeline reusable in enterprise environments.

Every detection rule was validated with multiple examples, and visualized through Splunk dashboards to aid in incident triage.

## 🔗 Access the Full Project

The complete project documentation, including detection rules and threat profiles is available on our GitHub repository:

👉 [View the full project on GitHub](https://github.com/Adamcalkins/Russian-Cyber-Threat-Detection)

**Authors**: [Szymon Czaus](https://zasushek.github.io) & Adam Cała<br>
**Date**: May 2025

Thanks for reading! If you’re interested in threat hunting or Splunk-based detection engineering, feel free to clone the repo and run the simulations in your lab environment.