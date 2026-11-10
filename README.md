# Agentic AI Security Lab

A hands on security lab built around Wazuh, n8n and AI assisted security operations.

I am following the [AtlantiumAI Agentic AI for Security Professionals masterclass](https://www.youtube.com/playlist?list=PLtyp1BBFawaz946JTxU1MOVZE13d37Yp7). This repository records my own build, configuration choices, tests, screenshots and troubleshooting.

A stage is only marked complete after I have built it and verified that it works.

## Lab progress

Stage 00 is the environment setup. The nine stages that follow cover the masterclass build.

| Stage | Focus | Masterclass lesson | Status |
|---|---|---|---|
| 00 | Ubuntu, Docker, Wazuh and n8n setup | Lesson 0 | Not started |
| 01 | Wazuh and n8n architecture with attack simulation | Lesson 1 | Not started |
| 02 | Auditd and Wazuh with Atomic Red Team | Lesson 2 | Not started |
| 03 | Wazuh API exploration with Postman | Lesson 3 | Not started |
| 04 | AI cybersecurity agent with n8n and Wazuh | Lesson 4 | Not started |
| 05 | EDR alert triage agent | Lesson 5 | Not started |
| 06 | Lab improvements for the threat hunter | Lesson 5.5 | Not started |
| 07 | Wazuh agents, Auditd and Sysmon telemetry | Lesson 5.6 | Not started |
| 08 | Attack chain simulation and investigation | Lesson 6 | Not started |
| 09 | AI threat hunter and model comparison | Lesson 7 | Not started |

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
| `docs/lessons/` | Build notes for each stage |
| `docs/` | Roadmap and project documentation |
| `screenshots/` | Visual evidence captured during testing |
| `workflows/` | Sanitised n8n workflow exports |
| `scripts/` | Scripts written for the lab |

## How I work

I build each stage, verify it, then document what actually happened. Planned work is labelled as planned. Untested commands are not presented as working instructions.

Screenshots and configuration examples must not expose passwords, API keys, tokens, private addresses or other sensitive information.

Attack simulation stays inside an isolated lab. No vulnerable service or test target will be exposed to the public internet.

I will prioritise local and free tooling. Any feature that could create a cloud charge or require a paid API will be checked before use.

## References

- [AtlantiumAI masterclass playlist](https://www.youtube.com/playlist?list=PLtyp1BBFawaz946JTxU1MOVZE13d37Yp7)
- [AtlantiumAI Wazuh and n8n lab setup](https://github.com/Atlantium-AI/wazuh-n8n-lab-setup)
