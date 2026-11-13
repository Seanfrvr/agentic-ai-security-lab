# Stage 05: EDR alert triage

Screenshots documenting the Postman query testing, OpenSearch aggregation configuration, Atomic Red Team activity, n8n workflow and successful triage execution.

## Postman query testing

| Screenshot | Evidence |
|---|---|
| [01 Testing aggregation queries](01-testing%20aggregation%20queries.png) | Count request against the Wazuh alert indices. The timestamp and rule level filters returned HTTP 200 with a count of 31. |
| [02 Search alert testing query](02-search%20alert%20testing%20query.png) | Search request for up to 100 alert records, sorted by timestamp descending, with selected source fields. |
| [03 Configuring search parameters](03-configuring%20search%20parameters.png) | OpenSearch terms aggregation configuration, including finding descriptions and commands. |
| [04 Configuring search parameters part 2](04-configuring%20search%20parameters%20pt2.png) | Additional aggregation buckets for destination users and packages. |

## Test activity and n8n workflow

| Screenshot | Evidence |
|---|---|
| [05 Atomic Red Team rerun](05-atomic%20red%20team%20rerun%20for%20more%20alerts.png) | Atomic Red Team test execution and cleanup output used to generate additional endpoint telemetry. |
| [06 Alert triage agent](06-alert%20triage%20agent.png) | n8n workflow showing the chat trigger, AI Agent, Gemini chat model, memory and Indexer HTTP Request tool. |
| [07 System prompt design](07-%20system%20prompt%20design.png) | Dynamic request body expression using `$fromAI()` to set the number of alerts and select relevant source fields. |
| [08 Aggregation configuration](08-aggregation%20config%20alert%202.png) | AI defined timestamp and rule level parameters in the Indexer search request. |

## Triage execution

| Screenshot | Evidence |
|---|---|
| [11 Triage testing final 1](11-%20triage%20testing%20finale%201.png) | Successful n8n execution and initial triage response. |
| [11 Triage testing final 2](11-triage%20testing%20finale%202.png) | Summary table separating high, medium and informational findings. |
| [11 Triage testing final 3](11-triage%20testing%20finale%203.png) | Detailed analysis of the Atomic Red Team rootkit and kernel module activity. |
| [Triage testing final 4](triage%20testing%20finale%204.png) | PAM configuration changes and routine operational events classified by priority. |
| [Triage testing final 5](triage%20testing%20finale%205.png) | Final assessment and analyst follow up recommendations. |

## Recorded execution

The captured execution completed successfully in 11.541 seconds and used 4,209 tokens. The agent identified Atomic Red Team activity, PAM configuration changes and routine system events, then recommended validating the testing context before treating the activity as malicious.
