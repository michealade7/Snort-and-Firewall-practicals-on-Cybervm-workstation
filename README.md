# Snort and Firewall Rules Lab

A GitHub-ready documentation workspace for the Cisco CyberOps **Lab – Snort and Firewall Rules** practical.

## Lab purpose
Practice monitoring IDS alerts with Snort, capturing traffic with `tcpdump`, and applying a firewall rule with `iptables` in the supplied CyberOps Workstation / Mininet environment.

## Required environment
- Oracle VirtualBox
- Cisco CyberOps Workstation VM
- Internet connection
- Mininet environment and lab support files supplied with the workstation

> **Important:** This lab is designed around CyberOps Workstation. Kali Linux is not a substitute for the supplied CyberOps VM. Keep your completed Kali/Scapy configuration unchanged unless a separate task requires changes.

## Repository structure

```text
Snort-Firewall-Rules-GitHub-Workflow/
├── README.md
├── docs/
│   └── lab-overview.md
├── workflow/
│   └── step-by-step-workflow.md
├── commands/
│   └── command-reference.md
├── evidence/
│   ├── screenshots/
│   │   └── README.md
│   └── terminal-output/
│       └── README.md
└── submission/
    └── lab-answers-template.md
```

## How to use this repository
1. Read `docs/lab-overview.md`.
2. Follow `workflow/step-by-step-workflow.md` in order.
3. Use `commands/command-reference.md` as a reference; run commands only at the prompt specified in the lab.
4. Save your own screenshots and terminal output in the evidence folders.
5. Complete `submission/lab-answers-template.md` using your actual lab observations.

## Evidence integrity
Do not create fake screenshots, logs, packet captures, or results. Capture evidence from your own VM. The lab's sample output is illustrative; your timestamps, packet counts, and process IDs may differ.

## Safety
The malware filename and server in this exercise are part of the isolated Cisco training topology. Do not download or execute malware on your host computer or outside the authorized lab environment. Keep the activity inside the provided CyberOps/Mininet lab.
