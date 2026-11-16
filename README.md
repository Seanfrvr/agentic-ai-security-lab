# Agentic AI Security Operations Lab

A local security operations lab built around Wazuh, n8n, OpenSearch and AI assisted analysis.

I use this environment to investigate endpoint telemetry, work with security APIs, build alert analysis workflows and explore how AI agents can support SOC tasks. The repository records the architecture, implementation, testing, troubleshooting and evidence from the lab.

A stage is only marked complete after it has been built and verified.

## Lab progress

| Stage | Focus | Documentation | Status |
|---|---|---|---|
| 00 | Ubuntu, Docker, Wazuh and n8n environment | [Lab setup](docs/lessons/lesson-00-lab-setup.md) | Complete |
| 01 | Wazuh and n8n architecture | [Architecture](docs/lessons/lesson-01-wazuh-n8n-architecture.md) | Complete |
| 02 | Auditd, Wazuh and Atomic Red Team | [Endpoint testing](docs/lessons/lesson-02-auditd-wazuh-atomic-red-team.md) | Complete |
| 03 | Wazuh API exploration with Postman | [API integration](docs/lessons/lesson-03-wazuh-api-postman.md) | Complete |
| 04 | AI cybersecurity agent with n8n and Wazuh | [Alert summarisation](docs/lessons/lesson-04-ai-cybersecurity-agent.md) | Complete |
| 05 | EDR alert triage agent | [Alert triage](docs/lessons/lesson-05-edr-alert-triage.md) | Complete |
| 06 | Lab improvements for the threat hunter | [Threat hunter improvements](docs/lessons/lesson-06-threat-hunter-lab-improvements.md) | Complete for lab foundation scope |
| 07 | Wazuh agents and Linux Auditd telemetry | [Endpoint telemetry](docs/lessons/lesson-07-endpoint-telemetry.md) | Complete for Linux telemetry scope |
| 08 | Web attack simulation and investigation | [Attack chain investigation](docs/lessons/lesson-08-attack-chain-investigation.md) | Complete for web investigation scope |
| 09 | AI threat hunter | [AI threat hunter](docs/lessons/lesson-09-ai-threat-hunter.md) | Complete for current investigation scope |

## Build approach

The lab follows the path from endpoint activity to security analysis:

1. Collect endpoint telemetry with Wazuh and Auditd.
2. Generate controlled test activity with Atomic Red Team and the vulnerable web application.
3. Access Wazuh data through its APIs and OpenSearch.
4. Build n8n workflows that retrieve and process security data.
5. Use AI models to summarise alerts and support triage.
6. Expand the environment toward threat hunting and attack chain investigation.

The current build includes a Wazuh alert summarisation agent, an aggregation based EDR triage agent and an AI threat hunting workflow. These use n8n and Google Gemini, with Wazuh Indexer providing access to alert data.

Stages 07 through 09 have been verified within their documented scope. Linux Auditd, authentication and system log telemetry is available in Wazuh. A controlled Kali to web application attack path has been investigated, and a custom Wazuh rule generates alerts for command parameter access. Windows telemetry, PowerShell activity, broader red team scenarios and a separate Linux privilege escalation target remain planned extensions.

## Repository structure

The tree below reflects the files currently committed to the repository.

```text
agentic-ai-security-lab/
├── docs/
│   ├── lessons/
│   │   ├── lesson-00-lab-setup.md
│   │   ├── lesson-01-wazuh-n8n-architecture.md
│   │   ├── lesson-02-auditd-wazuh-atomic-red-team.md
│   │   ├── lesson-03-wazuh-api-postman.md
│   │   ├── lesson-04-ai-cybersecurity-agent.md
│   │   ├── lesson-05-edr-alert-triage.md
│   │   ├── lesson-06-threat-hunter-lab-improvements.md
│   │   ├── lesson-07-endpoint-telemetry.md
│   │   ├── lesson-08-attack-chain-investigation.md
│   │   ├── lesson-09-ai-threat-hunter.md
│   │   └── lesson-template.md
│   └── roadmap.md
├── screenshots/
│   ├── 00-lab-setup/
│   ├── 02-auditd-atomic-red-team/
│   ├── 03-wazuh-api-postman/
│   ├── 04-ai-cybersecurity-agent/
│   ├── 05-edr-alert-triage/
│   ├── 06-threat-hunter-improvements/
│   ├── 07-endpoint-telemetry/
│   ├── 08-attack-chain-investigation/
│   ├── 09-ai-threat-hunter/
│   └── README.md
├── .gitignore
└── README.md
```

## Documentation and evidence

Each lesson page records its objective, architecture, implementation, testing results and limitations. Screenshots are stored by stage and linked selectively from the relevant lesson. Additional screenshots remain in their stage folders as supporting evidence rather than being embedded throughout the documentation.

The [screenshots directory](screenshots/) contains evidence for lab setup and Stages 02 through 09. Stage 09 evidence is stored in [09-ai-threat-hunter](screenshots/09-ai-threat-hunter/). Stage 01 has an architecture review in the lesson documentation, but does not currently have a dedicated screenshot folder.

See the [lab roadmap](docs/roadmap.md) for the planned sequence and verification goals.

## Lab principles

- **Local first:** prioritise local and free tooling. Check costs and usage limits before enabling services that could incur charges.
- **Evidence based:** document what was actually configured and tested. Keep planned work, failed attempts and verified results distinct.
- **Contained testing:** keep attack simulations and vulnerable targets inside the isolated lab environment.
- **Reproducibility:** record relevant versions, configuration choices and commands so the environment and tests can be understood and repeated.
- **Analyst led:** AI output supports investigation. Findings and recommendations require analyst review.

## About

An independently built home lab exploring Wazuh monitoring, endpoint detection, security automation, AI assisted alert triage and threat hunting.

## Phase 09 evidence

The [Phase 09 AI Threat Hunter screenshots](screenshots/09-ai-threat-hunter/) contain the supporting evidence for the workflow, investigation findings, Wazuh detections, MITRE ATT&CK mapping and final report.
