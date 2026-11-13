# Lab roadmap

Stage 00 prepares the local environment. Stages 01 to 09 follow the remaining lessons in the AtlantiumAI masterclass.

The stage numbers in this repository are sequential. The original lesson numbers are included so each page can be matched to the playlist.

## Build stages

| Stage | Masterclass lesson | Focus | What I will verify |
|---|---|---|---|
| 00 | Lesson 0 | Ubuntu, Docker, Wazuh and n8n setup | Services start, local access works and containers can communicate |
| 01 | Lesson 1 | Wazuh and n8n architecture with attack simulation | An isolated test produces telemetry that can be followed through Wazuh |
| 02 | Lesson 2 | Auditd and Wazuh integration with Atomic Red Team | Audit events are collected and controlled test activity is visible |
| 03 | Lesson 3 | Wazuh API exploration with Postman | Authentication works and selected API responses are understood |
| 04 | Lesson 4 | AI cybersecurity agent with n8n and Wazuh | The workflow receives security data and produces a traceable result |
| 05 | Lesson 5 | EDR alert triage agent | An alert is parsed, enriched and assessed with a recorded outcome |
| 06 | Lesson 5.5 | Lab improvements for the threat hunter | The changes required for the next stage are implemented and checked |
| 07 | Lesson 5.6 | Wazuh agents, Auditd and Sysmon telemetry | Endpoint sources send useful telemetry into the monitoring stack |
| 08 | Lesson 6 | Attack chain simulation and investigation | Each controlled action has corresponding evidence and an investigation timeline |
| 09 | Lesson 7 | AI threat hunter and model comparison | The agent is tested against defined cases and model results are compared fairly |

## Evidence standard

A stage should contain evidence that supports its claims.

1. Record the environment and versions used.
2. Explain the relevant architecture and data flow.
3. Include the commands and configuration that were actually used.
4. Show how the result was tested.
5. Include screenshots or output that support the result.
6. Record failures, fixes and limitations.
7. Explain security controls and any cost implications.

A stage remains **Not started** until work begins. It becomes **In progress** during the build and **Complete** only after its verification checks pass. If something only partly works, document that instead of marking the whole stage complete.

## Cost and isolation

Local and free options are the first choice. Check API pricing, usage limits and cloud billing before enabling any service that could incur charges.

Keep attack simulations and vulnerable targets inside the isolated lab environment.
