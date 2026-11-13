# Stage 04: AI Cybersecurity Agent

Evidence from the n8n workflow that retrieves Wazuh Indexer alerts and summarises them using Gemini 3.1 Flash.

| Screenshot | What it demonstrates |
|---|---|
| [01-configuring api requests.png](01-configuring%20api%20requests.png) | HTTP Request tool and Wazuh Indexer alert endpoint |
| [02-advanced agent parameters.png](02-advanced%20agent%20parameters.png) | AI-defined alert count and descending timestamp sort in the request body |
| [03-workflow setup.png](03-workflow%20setup.png) | Chat trigger, AI Agent, Gemini model, Simple Memory and connected tools |
| [04-alert summary analysis.png](04-alert%20summary%20analysis.png) | Successful execution and summary of the latest 20 alerts |

The execution evidence records 20 alerts retrieved, with 7 high, 8 medium and 5 low severity alerts. The workflow completed in 14.129 seconds and used 13,481 tokens.

