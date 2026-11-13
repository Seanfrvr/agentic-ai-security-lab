# Stage 04: AI cybersecurity agent

<sup>Status: In progress</sup>

## Objective

Build a conversational n8n agent that retrieves Wazuh alerts through the Indexer API and turns the results into a readable security summary with investigation guidance.

## Workflow

The workflow is named `First Wazuh Agent` and contains:

- **When chat message received:** starts the workflow from an analyst's chat message.
- **AI Agent:** interprets the request and coordinates the connected model, memory and tools.
- **Google Gemini Chat Model:** provides the agent's language model. This build uses Gemini 3.1 Flash.
- **Simple Memory:** provides conversational context.
- **Message a model in Google Gemini:** an additional Gemini node connected as a tool.
- **HTTP Request tool:** queries the Wazuh Indexer alert endpoint.

The workflow connects the chat trigger to the AI Agent. The model, memory and tools connect to the agent's dedicated input ports.

## Wazuh alert retrieval

The HTTP Request tool queries the Wazuh Indexer search API using the endpoint configured in the lab:

```text
https://172.19.0.4:9200/wazuh-alerts-4.x-*/_search
```

The address uses the Indexer container's IP on port `9200`, targets the `wazuh-alerts-4.x-*` index pattern and calls the `_search` endpoint. The IP is specific to the current Docker environment and may change if the container is recreated.

The request body uses an AI-defined `NumAlerts` parameter through n8n's `$fromAI()` expression. The captured expression supplies a default of 10 when the agent does not provide a value. The query sorts results by `@timestamp` in descending order and selects source fields for the response.

The configuration screenshot shows the request method as `GET`. The successful execution screenshot confirms that the request tool ran and returned data.

## Verification

The workflow was tested through the n8n chat interface with a request to retrieve and summarise the latest 20 alerts.

The captured execution shows:

| Result | Observed value |
|---|---:|
| Alerts retrieved | 20 |
| High severity, level 10 | 7 |
| Medium severity, level 7 | 8 |
| Low severity, level 3 | 5 |
| Execution duration | 14.129 seconds |
| Token usage | 13,481 |

The returned summary highlighted suspicious network interface activity involving promiscuous mode on the `ubuntu-local` endpoint (agent `007`).

The execution view shows the chat trigger, AI Agent, Gemini model, memory and HTTP Request tool completing successfully.

## Evidence

- [HTTP Request configuration](../../screenshots/04-ai-cybersecurity-agent/01-configuring%20api%20requests.png)
- [Dynamic alert count and query body](../../screenshots/04-ai-cybersecurity-agent/02-advanced%20agent%20parameters.png)
- [Workflow architecture](../../screenshots/04-ai-cybersecurity-agent/03-workflow%20setup.png)
- [Successful alert summary and execution](../../screenshots/04-ai-cybersecurity-agent/04-alert%20summary%20analysis.png)

## Findings and next checks

The initial end-to-end workflow is operational. The captured result demonstrates alert retrieval and AI-assisted summarisation, not autonomous remediation. Recommendations produced by the agent still require analyst review.

The exact local authentication and TLS configuration, full query details and error handling can be examined in a later build or validation pass. The current evidence is sufficient to record the successful initial integration.

## Outcome

Initial workflow built and successfully executed. Further validation can be carried into the next phase.

## Next stage

[Stage 05: EDR alert triage](lesson-05-edr-alert-triage.md)
