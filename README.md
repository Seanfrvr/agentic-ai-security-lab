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
| 06 | Lab improvements for the threat hunter | [Threat hunter improvements](docs/lessons/lesson-06-threat-hunter-lab-improvements.md) | In progress |
| 07 | Wazuh agents, Auditd and Sysmon telemetry | [Endpoint telemetry](docs/lessons/lesson-07-endpoint-telemetry.md) | Not started |
| 08 | Attack chain simulation and investigation | [Attack chain investigation](docs/lessons/lesson-08-attack-chain-investigation.md) | Not started |
| 09 | AI threat hunter and model comparison | [AI threat hunter](docs/lessons/lesson-09-ai-threat-hunter.md) | Not started |

## Build approach

The lab follows the path from endpoint activity to security analysis:

1. Collect endpoint telemetry with Wazuh and Auditd.
2. Generate controlled test activity with Atomic Red Team.
3. Access Wazuh data through its APIs and OpenSearch.
4. Build n8n workflows that retrieve and process security data.
5. Use AI models to summarise alerts and support triage.
6. Expand the environment toward threat hunting and attack chain investigation.

The current build includes a Wazuh alert summarisation agent and an aggregation based EDR triage agent. Both use n8n and Google Gemini, with Wazuh Indexer providing the alert data.\n\nStage 06 is underway. A Docker hosted vulnerable web application has been added to the Ubuntu lab, and its harmless `whoami` HTTP request has been verified in the Wazuh archives index. Detection development and further attack simulation remain future work.\n\nStage 06 is underway. A Docker hosted vulnerable web application has been added to the Ubuntu lab, and its harmless `whoami` HTTP request has been verified in the Wazuh archives index. Detection development and further attack simulation remain future work.

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
│   └── README.md
├── .gitignore
└── README.md
```

## Documentation and evidence

Each lesson page records its objective, architecture, implementation, testing results and limitations. Screenshots are stored by stage and linked from the relevant lesson.

The [screenshots directory](screenshots/) contains evidence for lab setup and Stages 02 through 05. Stage 06 evidence notes are in place, with screenshots pending transfer and review. Stage 01 has an architecture review in the lesson documentation, but does not currently have a dedicated screenshot folder.

See the [lab roadmap](docs/roadmap.md) for the planned sequence and verification goals.

## Lab principles

- **Local first:** prioritise local and free tooling. Check costs and usage limits before enabling services that could incur charges.
- **Evidence based:** document what was actually configured and tested. Keep planned work, failed attempts and verified results distinct.
- **Contained testing:** keep attack simulations and vulnerable targets inside the isolated lab environment.
- **Reproducibility:** record relevant versions, configuration choices and commands so the environment and tests can be understood and repeated.
- **Analyst led:** AI output supports investigation. Findings and recommendations require analyst review.

## About

An independently built home lab exploring Wazuh monitoring, endpoint detection, security automation, AI assisted alert triage and threat hunting.
