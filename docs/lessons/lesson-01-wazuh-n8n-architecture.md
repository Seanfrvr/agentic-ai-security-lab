# Stage 01: Wazuh and n8n architecture

<sup>Status: Complete</sup>

## Objective

Document how endpoint telemetry moves through Wazuh and how n8n uses the resulting security data in automated workflows.

## Architecture

| Component | Responsibility |
|---|---|
| Wazuh Agent | Collects endpoint telemetry |
| Wazuh Manager | Receives and analyses agent events, applies rules and generates alerts |
| Wazuh Indexer | Stores and indexes security data |
| Wazuh Dashboard | Provides an interface for reviewing alerts, agents and security data |
| n8n | Connects to APIs and orchestrates security workflows |

## Data flow

1. An endpoint generates activity collected by its Wazuh Agent.
2. The agent forwards events to the Wazuh Manager.
3. The Manager analyses events and generates alerts when rules match.
4. The Indexer stores the resulting security data.
5. An analyst reviews alerts and endpoint activity through the Wazuh Dashboard.
6. n8n queries security data through the Wazuh Indexer API and uses the results in automation workflows.

<text></text>

## Lab implementation

The local environment runs four containers:

| Component | Version or image |
|---|---|
| Wazuh Manager | 4.9.0 |
| Wazuh Indexer | 4.9.0 |
| Wazuh Dashboard | 4.9.0 |
| n8n | `n8nio/n8n` |

The containers share the Docker network `soc-net`. The environment setup and container verification are documented in [Stage 00: Lab setup](lesson-00-lab-setup.md).

## Integration

The Wazuh APIs were explored with Postman, and n8n was configured to retrieve alert data from the Wazuh Indexer. The integration was then used in the AI agent and alert triage workflows.

Implementation evidence:

- [Stage 03: Wazuh API and Postman](lesson-03-wazuh-api-postman.md)
- [Stage 04: AI cybersecurity agent](lesson-04-ai-cybersecurity-agent.md)
- [Stage 05: EDR alert triage](lesson-05-edr-alert-triage.md)

## Outcome

The component roles and data flow are documented. The shared Docker environment supports Wazuh API access from Postman and n8n, with the integration demonstrated in the subsequent workflow stages.

## Next stage

[Stage 02: Auditd and Atomic Red Team](lesson-02-auditd-wazuh-atomic-red-team.md)
