# Hack The Box SOC Notes

Personal cybersecurity study notes based on Hack The Box Academy content, organized as a growing reference for security operations, Linux, networking, and web application security.

## Contents

| Track | Scope | Entry point |
| --- | --- | --- |
| **Cybersecurity Analyst** | Information security concepts and network foundations | [Open the track](CybersecurityAnalyst/_CYBERSECURITY-ANALYST.md) |
| **Linux Fundamentals** | Shell usage, filesystems, permissions, services, networking, logs, and administration | [Open the track](LinuxFundamentals/_Linux.md) |
| **SOC Analyst** | Incident handling, SIEM, threat hunting, network traffic analysis, Windows telemetry, detection engineering, malware analysis, and digital forensics | [Open the track](SOC/_SOC-ANALYST.md) |
| **Web Applications** | Web architecture, frontend and backend technologies, databases, APIs, and common web vulnerabilities | [Open the track](WebApplications/_WEB-APPLICATIONS.md) |

## What You Will Find

- Fundamentals of information security, networking, and Linux systems.
- SOC workflows covering preparation, detection and analysis, containment, eradication, recovery, and post-incident activity.
- Practical security operations topics including SIEM use cases, alert triage, Splunk, Elastic, Suricata, Snort, Zeek, Sysmon, and Windows Event Logs.
- Threat hunting, threat intelligence, MITRE ATT&CK operations, network traffic analysis, and digital forensics.
- Web application fundamentals and introductory coverage of issues such as sensitive data exposure, injection, cross-site scripting, and cross-site request forgery.

## Repository Layout

```text
.
├── CybersecurityAnalyst/   # Information security and network foundations
├── LinuxFundamentals/      # Linux administration and troubleshooting notes
├── SOC/                    # Security operations and incident response notes
├── WebApplications/        # Web technologies and application security notes
└── README.md
```

Each track contains an index file and topic-specific Markdown notes. The index files provide the intended reading order and navigation between related topics.

## How to Use This Repository

1. Start with the index for the track you want to study.
2. Follow the linked topics in sequence, or use the notes as a reference during investigations and labs.
3. Add commands, explanations, examples, and lessons learned to the relevant topic rather than creating duplicate notes.
4. Keep links relative to the repository so the notes remain portable across GitHub, VS Code, and Markdown knowledge-base tools.

The notes use Markdown, and several index files use Obsidian-style `[[page-name]]` links. A Markdown editor or knowledge-base application that supports those links provides the best local navigation experience.

Answers to Hack The Box questions and practical exercises are intentionally not included. This keeps the repository focused on learning and practice, while avoiding the risk of enabling plagiarism or causing academic and platform-related issues.

## Contributing Notes

There is no application to build and no dependency installation required. Changes should remain focused on study content and preserve the existing organization:

- Use clear topic-focused filenames in lowercase with hyphens.
- Update the relevant track index when adding a topic.
- Prefer concise explanations supported by commands, examples, diagrams, or references where useful.
- Correct technical inaccuracies and broken links when they are found.
- Do not include secrets, live credentials, or sensitive data from labs or real environments.

## Status

This is an actively evolving personal learning repository. Coverage and depth vary by topic; the track indexes are the best way to see the current scope.
