# Stage 09: AI Threat Hunter

<sup>Status: Complete for the current investigation scope</sup>

## Objective

Build an AI threat hunting workflow that accepts investigation questions through n8n, queries Wazuh data and produces structured findings with supporting evidence, MITRE ATT&CK context and remediation recommendations.

The aim was to give an analyst a practical way to investigate security activity and turn relevant results into clear reports. The agent must distinguish evidence from interpretation and identify where the available data does not support a firm conclusion.

## Architecture

The workflow uses an n8n AI Agent connected to Google Gemini 2.5 Flash. An analyst submits a question through the chat interface. The agent uses an HTTP Request tool to query the Wazuh Indexer API and then prepares an investigation response.

| Component | Role |
|---|---|
| n8n Chat Trigger | Receives investigation questions |
| n8n AI Agent | Coordinates the investigation |
| Google Gemini 2.5 Flash | Analyses the available results and prepares the report |
| HTTP Request tool | Queries the Wazuh Indexer API |
| Wazuh Indexer | Provides indexed alerts and security events |
| Conversation memory | Retains conversational context |

The workflow supports analyst investigation. It does not automatically isolate endpoints, disable accounts or make changes to the environment.

![AI Threat Hunter workflow](../../screenshots/09-ai-threat-hunter/01-ai-threat-hunter-workflow.png)

## Agent configuration

The agent was configured for SOC threat hunting and DFIR analysis. Its instructions guide it to investigate suspicious activity, identify affected systems, correlate relevant events and present findings with supporting evidence.

The instructions also require it to distinguish attempted activity from confirmed execution, avoid unsupported claims, identify evidence gaps and recommend practical remediation. MITRE ATT&CK techniques should only be included where the available findings support the mapping.

![AI agent configuration](../../screenshots/09-ai-threat-hunter/02-agent%20message%20and%20role%20assign.png)

## Investigation and findings

The workflow was tested with questions covering suspicious activity, command execution, initial access, post compromise activity and the wider attack chain. The agent returned investigation findings, supporting evidence and remediation guidance.

![Investigation findings](../../screenshots/09-ai-threat-hunter/04-incident%20findings.png)

The investigation drew on Wazuh data collected during the earlier endpoint and web attack stages. One important detection was custom Rule ID `100100`, titled `Web application command parameter accessed`. It is a Level 8 rule that identifies requests accessing the vulnerable application's `cmd` parameter. Eight matching alerts were observed.

This rule identifies access to the command parameter. On its own, it does not prove that every requested command executed successfully or that privilege escalation occurred.

An Indexer query returned 38 matching records for `ubuntu-local`: 30 records titled `Auditd: Device enables promiscuous mode.` and eight records titled `Web application command parameter accessed`. The response contained aggregation results but no individual event documents. These two finding types were therefore kept separate rather than treated as one attack sequence.

![Wazuh detections](../../screenshots/09-ai-threat-hunter/09-wazuh%20detections.png)

## MITRE ATT&CK and evidence gaps

The agent was asked to map relevant activity to MITRE ATT&CK without treating a possible technique as proof of successful compromise. The investigation considered exploitation of the vulnerable web application, command execution and file or system discovery.

For example, searching for SUID files is file and directory discovery. It does not establish privilege escalation. The investigation did not establish container escape, compromise of the Ubuntu host, persistence, credential theft or lateral movement.

The available Indexer response did not always include individual event documents or the fields needed to independently reconstruct each command execution. Findings therefore had to be assessed within the limits of the returned data and the earlier lab evidence.

![MITRE ATT&CK mapping](../../screenshots/09-ai-threat-hunter/10-mitre%20attack%20mappings.png)

## Final investigation report

The final prompt asked the agent to consolidate the investigation into a DFIR report covering the attack, confirmed findings, affected systems, security impact, Wazuh detections, severity and recommended remediation.

![Final investigation report](../../screenshots/09-ai-threat-hunter/12-incident%20report.png)

## Evaluation and limitations

The workflow was exercised with multiple investigation questions and report formats. It demonstrated how an AI agent can query Wazuh data and help organise findings, evidence, ATT&CK references and remediation guidance.

Testing used Google Gemini 2.5 Flash. A controlled comparison with other models, formal prompt injection testing and a structured assessment of resource use and API cost were not completed.

The quality of the response depends on the data returned by the Indexer and the accuracy of the agent's analysis. Where individual event records are unavailable, the agent cannot independently validate every detail. Analyst review remains necessary before treating its conclusions as confirmed incident findings or taking action.

## Outcome

The AI Threat Hunter workflow is implemented and has been exercised against the web attack investigation documented in Stage 08. It accepts analyst questions, queries the Wazuh Indexer through n8n and generates structured investigation reports.

The workflow provides an investigation interface over the lab's security data while keeping evidence limitations and analyst review in view.

## Project conclusion

This stage brings the lab from endpoint telemetry and Wazuh detection into AI supported threat hunting. The current environment provides a foundation for investigating Linux activity and a controlled web application attack.

The next improvements will expand the red team activity in the lab and introduce more varied attack scenarios. I also plan to bring the Windows virtual machine into the investigation workflow, with PowerShell activity and Windows endpoint telemetry providing additional material for detection, correlation and threat hunting. This will broaden the lab beyond its current Linux focused investigation scope.
