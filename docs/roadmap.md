# Lab roadmap

This repository follows the ten stages in the AtlantiumAI masterclass. The lesson pages will record my own implementation rather than copy the instructor's steps without testing them.

## Stages

| Stage | Masterclass topic | What I will document |
|---|---|---|
| 00 | Lab setup for agentic AI security automation | Ubuntu environment, Docker setup, Wazuh services, n8n and container networking |
| 01 | Wazuh and n8n architecture with attack simulation | How the services connect, where alerts move and how the test activity appears in Wazuh |
| 02 | Auditd and Wazuh integration with Atomic Red Team | Linux audit telemetry, Wazuh collection and controlled test results |
| 03 | Exploring the Wazuh API with Postman | API authentication, useful endpoints and verified API responses |
| 04 | Building an AI cybersecurity agent | The n8n workflow, inputs, processing steps, model connection and output |
| 05 | EDR alert triage AI agent | Alert input, enrichment, triage logic and the resulting investigation summary |
| 05.5 | Improving the lab for an AI threat hunter | Changes to the lab and why they are needed for the next stage |
| 05.6 | Wazuh agents, Auditd and Sysmon | Endpoint coverage, agent configuration and the telemetry collected |
| 06 | Reconnaissance, pivoting, exploitation and privilege escalation | Isolated attack simulation, event evidence and investigation timeline |
| 07 | AI threat hunter 1.0 and model comparison | Agent workflow, test cases, model behaviour and comparison results |

## How each stage will be recorded

Each lesson page will contain the parts that apply to that stage:

1. Objective
2. Environment and prerequisites
3. Architecture or data flow
4. Commands and configuration used
5. Verification and test results
6. Screenshots and other evidence
7. Problems and fixes
8. Security notes
9. What worked and what did not
10. Next stage

I will record actual commands and settings after running them. Anything that has not been tested will be labelled as planned or pending.

## Cost and safety

The first choice is local tooling and free options. Any step that could create cloud charges, require a paid API or start a subscription will be checked before it is used.

Attack simulation will remain inside the lab. No vulnerable service or test target will be exposed to the public internet.
