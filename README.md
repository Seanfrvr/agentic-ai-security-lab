# Agentic AI Security Lab

A hands on security lab built around Wazuh, n8n and AI assisted security operations.

The work follows the [AtlantiumAI Agentic AI for Security Professionals masterclass](https://www.youtube.com/playlist?list=PLtyp1BBFawaz946JTxU1MOVZE13d37Yp7). I am documenting what I build, the decisions I make, the problems I run into and the evidence from each stage.

This is a work in progress. A lesson is only marked complete after I have built and tested the relevant parts myself.

## Lab progress

| Stage | Focus | Status |
|---|---|---|
| 00 | Lab setup with Ubuntu, Docker, Wazuh and n8n | Not started |
| 01 | Wazuh and n8n architecture with attack simulation | Not started |
| 02 | Auditd and Wazuh integration with Atomic Red Team | Not started |
| 03 | Wazuh API exploration with Postman | Not started |
| 04 | AI cybersecurity agent with n8n and Wazuh | Not started |
| 05 | EDR alert triage agent | Not started |
| 05.5 | Lab improvements for the threat hunter | Not started |
| 05.6 | Wazuh agents, Auditd and Sysmon telemetry | Not started |
| 06 | Attack chain simulation and investigation | Not started |
| 07 | AI threat hunter and model comparison | Not started |

## Documentation

- [Lab roadmap](docs/roadmap.md)
- [Lesson 00: Lab setup](docs/lessons/lesson-00-lab-setup.md)
- [Lesson documentation template](docs/lessons/lesson-template.md)

## Lab approach

The lab is being built and tested in stages. Screenshots, configuration examples, test results and troubleshooting notes will be added as the work progresses.

All attack simulation will stay inside an isolated lab environment. Credentials, API keys, tokens and other sensitive values will not be published.

The goal is to understand how the components work together, not just reproduce a workflow from a video.

## Reference

[AtlantiumAI masterclass playlist](https://www.youtube.com/playlist?list=PLtyp1BBFawaz946JTxU1MOVZE13d37Yp7)

[AtlantiumAI Wazuh and n8n lab setup repository](https://github.com/Atlantium-AI/wazuh-n8n-lab-setup)
