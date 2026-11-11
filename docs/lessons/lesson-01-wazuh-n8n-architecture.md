# Stage 01: Wazuh and n8n architecture

<sup>Status: Reference reviewed; practical validation not started</sup>

**Masterclass reference:** Lesson 1, *Wazuh + n8n Architecture & Attack Simulation*

## Objective

Understand the role of each component in the lab and how endpoint security events can move through Wazuh before n8n uses the Wazuh API to support automated security operations.

## Lesson scope

This video is an architecture walkthrough. It explains the environment and the intended interaction between its components; it does not walk through a new build or produce practical test evidence.

No additional screenshots were captured for this lesson. The environment screenshots are recorded under [Stage 00: Lab setup](lesson-00-lab-setup.md).

## Architecture

| Component | Responsibility |
|---|---|
| Wazuh Agent | Collects endpoint telemetry |
| Wazuh Manager | Receives and analyses agent events, applies rules and generates alerts |
| Wazuh Indexer | Stores and indexes security data |
| Wazuh Dashboard | Allows an analyst to review alerts, agents and security data |
| n8n | Connects to services through integrations and HTTP requests, then orchestrates workflows and agent actions |

## Intended data flow

1. An endpoint produces activity that is collected by its Wazuh Agent.
2. The agent forwards events to the Wazuh Manager.
3. The Manager analyses the events and generates alerts where its rules match.
4. The Indexer stores the resulting security data.
5. An analyst reviews the data through the Wazuh Dashboard.
6. n8n can query the Wazuh API through HTTP requests and use the returned information in an automation workflow.

The video also introduces Auditd and Atomic Red Team as tools for generating and collecting security telemetry in later practical lessons. Their integration and attack simulations are not part of this architecture-only walkthrough.

## Current lab state

The local environment currently has four running containers:

- Wazuh Manager 4.9.0
- Wazuh Indexer 4.9.0
- Wazuh Dashboard 4.9.0
- n8n using the `n8nio/n8n` image

The three Wazuh containers were connected to the shared Docker network `soc-net`. n8n was started using a Compose file that also references this external network.

Container startup and shared network attachment do not, by themselves, prove that n8n can successfully authenticate to or retrieve data from the Wazuh API. That application-level test remains outstanding.

## Practical validation

The following work remains for the later build stages:

- Verify the Wazuh Manager API is reachable from n8n.
- Configure authentication without exposing credentials in workflow exports or screenshots.
- Retrieve a controlled example of Wazuh data through an n8n HTTP Request node.
- Configure endpoint telemetry with Auditd.
- Run an authorised, isolated Atomic Red Team test and trace the resulting event through Wazuh.
- Record the alert and any subsequent workflow activity.

## Evidence

No separate screenshots are required for this architecture explanation. Practical evidence will be captured when the connections, telemetry and simulations are tested.

## Findings and troubleshooting

The existing Wazuh deployment is version 4.9.0, while the instructor's setup script targets 4.12.0. The existing deployment was retained rather than replaced. The network mismatch was resolved by creating `soc-net` and connecting the three existing Wazuh containers to it.

## Outcome

The architecture and intended data flow have been reviewed. Practical integration and attack simulation have not yet been verified.

## Next stage

[Stage 02: Auditd and Atomic Red Team](lesson-02-auditd-wazuh-atomic-red-team.md)
