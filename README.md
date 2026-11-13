# Agentic AI Security Lab

My personal home lab for exploring and engineering security operations workflows with Wazuh, n8n and AI assisted analysis.

The lab is built and tested in my own local environment. I use it to investigate endpoint telemetry, detection and response, security automation, threat hunting and the safe use of AI agents in security workflows. This repository documents my architecture, implementation decisions, commands, tests, troubleshooting and verified results.

A stage is only marked complete after I have built it and verified that it works.

## Lab progress

Stage 00 covers the local home lab environment. The remaining stages expand its monitoring, detection and automation capabilities.

| Stage | Focus | Reference | Status |
|---|---|---|---|
| 00 | Ubuntu, Docker, Wazuh and n8n environment | Setup notes | In progress |
| 01 | Wazuh and n8n architecture | Architecture review | Reviewed |
| 02 | Auditd and Wazuh with Atomic Red Team | Build 02 | In progress |
| 03 | Wazuh API exploration with Postman | Build 03 | In progress |
| 04 | AI cybersecurity agent with n8n and Wazuh | Build 04 | Not started |
| 05 | EDR alert triage agent | Build 05 | Not started |
| 06 | Lab improvements for the threat hunter | Build 06 | Not started |
| 07 | Wazuh agents, Auditd and Sysmon telemetry | Build 07 | Not started |
| 08 | Attack chain simulation and investigation | Build 08 | Not started |
| 09 | AI threat hunter and model comparison | Build 09 | Not started |

## Build sequence

The project follows the flow from endpoint telemetry to AI assisted security operations: collect activity with Auditd and Wazuh, expose Wazuh data through its APIs, analyse it with n8n and an AI model, then build toward alert triage and threat hunting. Each stage records the implementation and evidence from the local lab.

## Documentation

- [Lab roadmap](docs/roadmap.md)
- [Stage 00: Lab setup](docs/lessons/lesson-00-lab-setup.md)
- [Stage 01: Wazuh and n8n architecture](docs/lessons/lesson-01-wazuh-n8n-architecture.md)
- [Stage 02: Auditd and Atomic Red Team](docs/lessons/lesson-02-auditd-wazuh-atomic-red-team.md)
- [Stage 03: Wazuh API and Postman](docs/lessons/lesson-03-wazuh-api-postman.md)
- [Stage 04: AI cybersecurity agent](docs/lessons/lesson-04-ai-cybersecurity-agent.md)
- [Stage 05: EDR alert triage](docs/lessons/lesson-05-edr-alert-triage.md)
- [Stage 06: Threat hunter lab improvements](docs/lessons/lesson-06-threat-hunter-lab-improvements.md)
- [Stage 07: Endpoint telemetry](docs/lessons/lesson-07-endpoint-telemetry.md)
- [Stage 08: Attack chain investigation](docs/lessons/lesson-08-attack-chain-investigation.md)
- [Stage 09: AI threat hunter](docs/lessons/lesson-09-ai-threat-hunter.md)

## Repository structure

| Path | Purpose |
|---|---|
| `docs/lessons/` | Build notes, implementation decisions and test results |
| `docs/` | Roadmap and project documentation |
| `screenshots/` | Visual evidence captured during lab setup and testing |
| `workflows/` | Sanitised n8n workflow exports |
| `scripts/` | Scripts written for the lab |

## Lab principles

- **Local first:** prioritise local and free tooling. Check any feature that could create a cloud charge or require a paid API before using it.
- **Evidence based:** document what was actually configured and tested. Keep planned work, failed attempts and verified results clearly distinguished.
- **Secure by design:** do not commit passwords, API keys, tokens, private keys, credentials or sensitive configuration. Review screenshots, logs and workflow exports before committing.
- **Contained testing:** keep attack simulations and vulnerable targets inside the isolated lab. Do not expose them to the public internet.
- **Reproducibility:** record relevant versions, configuration choices and commands so the environment and tests can be understood and repeated.

## Project approach

This is an independently built security operations home lab. The repository documents the architecture, configurations, integrations, simulations, troubleshooting and validation carried out in the environment. Each result is based on hands-on testing, with relevant technical details and evidence recorded as the lab develops.
