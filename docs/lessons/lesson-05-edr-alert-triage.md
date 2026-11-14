# Stage 05: EDR alert triage

<sup>Status: Complete</sup>

## Objective

Build an AI assisted triage workflow that groups Wazuh alert data before sending it to an LLM. The aim is to reduce repetitive raw event context and help the analyst identify high priority activity, configuration changes and routine noise.

## Architecture

The workflow uses the local Wazuh stack, n8n, OpenSearch and a Google Gemini chat model.

1. Wazuh collects endpoint telemetry and generates alerts.
2. n8n sends a POST search request to the Wazuh Indexer.
3. OpenSearch filters the alert data and returns aggregation buckets.
4. The AI agent reviews the grouped results and produces a triage assessment with investigation recommendations.

The workflow is named **Alert Triage agent**. It contains a chat trigger, AI Agent, Google Gemini Chat Model, Simple Memory, a Gemini model tool and an HTTP Request tool connected to the Indexer.

## Indexer queries

Postman was used to validate the Indexer queries before connecting them to n8n.

The count request used:

`POST {{baseUrl-Indexer}}/wazuh-alerts-*/_count`

The query filtered alerts by timestamp and rule level. The captured response returned HTTP 200 and a count of **31**.

A separate search request used:

`POST {{baseUrl-Indexer}}/wazuh-alerts-4.x-*/_search`

The search requested up to 100 records, sorted by `@timestamp` in descending order, and selected relevant source fields including timestamp, agent details, rule details and the full log.

The endpoint aggregation request grouped alert data using terms aggregations. The visible configuration includes buckets for finding descriptions (`rule.description`), commands (`data.command`), destination users (`data.dstuser`) and packages (`data.package`). The query configuration also includes endpoint information.

## n8n implementation

The previous agent workflow was cloned and adapted into **Alert Triage agent**.

The HTTP Request tool uses POST against the Wazuh alert search endpoint:

`/wazuh-alerts-4.x-*/_search`

The request body uses OpenSearch query and aggregation structures. AI defined parameters are supplied through n8n expressions using `$fromAI()`:

- Start and end timestamps for the search window.
- Lower and upper Wazuh rule level bounds.
- A configurable time zone in the timestamp range.

The captured expression preview shows a timestamp range and rule level range. The visible time zone setting is `America/Denver`. The alert triage workflow also uses a dedicated system prompt that asks the agent to prioritise findings and distinguish them from likely operational noise.

## Test activity

Atomic Red Team tests were rerun to generate additional endpoint activity for the triage workflow. The terminal screenshot records execution and cleanup output for multiple tests, including tests associated with rootkit and process memory techniques.

## Validation results

The agent was tested with the chat request:

> Hey can you triage all my alerts from the last 24 hours. What should I focus on and what is most likely noise

The captured n8n execution completed successfully in **11.541 seconds** and used **4,209 tokens**.

The resulting assessment grouped the observed activity into three categories:

| Priority | Observed activity | Triage interpretation |
|---|---|---|
| High | Atomic Red Team execution and kernel module manipulation | Commands including `rmmod`, `modprobe -r` and removal of kernel module files were associated with rootkit and persistence testing activity. |
| Medium | PAM and sudo configuration changes | A backup file was copied into `/etc/pam.d/password-auth`. This warrants verification if it is not part of the authorised test activity. |
| Informational | Routine operating system activity | Login and logout events, Auditd and SELinux diagnostics, and Wazuh agent or server lifecycle events were treated as likely noise in this test context. |

The detailed response recommended confirming whether red team or security testing was scheduled, verifying the source of the root activity, reviewing the scope of the tests and documenting confirmed authorised activity.

The agent did not execute remediation or independently verify authorisation. Its output is an analyst aid and the underlying events still require review.

## Findings and limitations

- Aggregations reduce the need to pass repeated raw alert records into the model, but empty aggregation buckets can still add noise to the returned context.
- The captured workflow relies on the model to interpret priority. Explicit escalation thresholds and deterministic decision rules remain potential improvements.
- The final assessment correctly treated the activity as suspicious in isolation while acknowledging the Atomic Red Team test context. This is an important distinction between suspicious telemetry and confirmed malicious activity.
- A successful agent response does not by itself establish that every alert was retrieved or that the triage conclusions are complete.

## Selected screenshots

A few key views are included here so the implementation and results are visible while reading the lesson.

### OpenSearch aggregation configuration

![OpenSearch aggregation query configuration](../../screenshots/05-edr-alert-triage/03-configuring%20search%20parameters.png)

### n8n alert triage workflow

![Alert Triage agent workflow in n8n](../../screenshots/05-edr-alert-triage/06-alert%20triage%20agent.png)

### Triage summary

![AI triage summary separating high, medium and informational findings](../../screenshots/05-edr-alert-triage/11-triage%20testing%20finale%202.png)

### Final assessment and analyst follow up

![Final triage assessment and recommended analyst follow up](../../screenshots/05-edr-alert-triage/triage%20testing%20finale%205.png)

## Evidence

The [Stage 05 screenshot evidence](../../screenshots/05-edr-alert-triage/README.md) records the Postman queries, aggregation configuration, Atomic Red Team activity, n8n workflow and final triage output.

## Outcome

The initial aggregation based EDR triage workflow is complete and successfully tested. Further refinement of aggregation output and explicit triage thresholds can be considered as future improvements.

## Next stage

[Stage 06: Threat hunter lab improvements](lesson-06-threat-hunter-lab-improvements.md)
