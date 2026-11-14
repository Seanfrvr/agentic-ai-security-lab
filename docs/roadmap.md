# Lab roadmap

This roadmap tracks the development of the Agentic AI Security Lab, from the local infrastructure through endpoint monitoring, security automation, alert triage and AI assisted threat hunting.

The stages are organised around the build sequence and the capabilities being implemented in the lab.

## Build stages

| Stage | Focus | What I will verify |
|---|---|---|
| 00 | Ubuntu, Docker, Wazuh and n8n environment | Services start, local access works and containers can communicate |
| 01 | Wazuh and n8n architecture with attack simulation | An isolated test produces telemetry that can be followed through Wazuh |
| 02 | Auditd and Wazuh integration with Atomic Red Team | Audit events are collected and controlled test activity is visible |
| 03 | Wazuh API exploration with Postman | Authentication works and selected API responses are understood |
| 04 | AI cybersecurity agent with n8n and Wazuh | The workflow retrieves security data and produces a traceable summary |
| 05 | EDR alert triage agent | Aggregated alert data is assessed and returned with prioritised findings |
| 06 | Lab improvements for threat hunting | Improvements to the lab are implemented and checked |
| 07 | Wazuh agents, Auditd and Sysmon telemetry | Endpoint sources send useful telemetry into the monitoring stack |
| 08 | Attack chain simulation and investigation | Controlled activity can be correlated into an investigation timeline |
| 09 | AI threat hunter and model comparison | The agent is tested against defined cases and model results are compared |

## Evidence standard

Each stage should contain evidence that supports its implementation and results.

1. Record the environment and relevant versions.
2. Explain the architecture and data flow.
3. Include the commands and configuration actually used.
4. Show how the implementation was tested.
5. Include screenshots or output that support the results.
6. Record failures, fixes and known limitations.
7. Explain relevant security controls and cost implications.

A stage remains **Not started** until work begins. It becomes **In progress** during implementation and **Complete** only after its verification checks pass. If a component only partly works, document that accurately rather than marking the entire stage complete.

## Cost and isolation

Local and free tooling are preferred. Check API pricing, usage limits and cloud billing before enabling any service that could incur charges.

Keep attack simulations and vulnerable targets inside the isolated lab environment.
