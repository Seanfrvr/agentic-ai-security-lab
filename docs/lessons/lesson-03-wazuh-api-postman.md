# Stage 03: Wazuh API and Postman

<sup>Status: In progress</sup>

**Masterclass reference:** Lesson 3, *Exploring the Wazuh API with Postman*

## Objective

Test how Wazuh data can be accessed programmatically. Postman was used to authenticate with the Wazuh Manager API, inspect endpoint information and query alert data through the Wazuh Indexer API. These are the same interfaces the n8n agent will use in the next stages.

## API architecture

| Component | Address in the lab | Purpose |
|---|---|---|
| Wazuh Manager API | Port `55000` | Manager operations and endpoint information |
| Wazuh Indexer API | Port `9200` | Search and retrieve indexed alert records |
| Postman | Ubuntu lab environment | Send requests and inspect API responses |

The Manager API and Indexer API serve different purposes. The Manager API provides information about managed agents and their inventory. The Indexer API provides search access to stored Wazuh alert data.

## Authentication

### Wazuh Manager API

A POST authentication request was tested in Postman. The request returned **HTTP 200** and a JSON Web Token. A Postman script stores the returned token for use in later requests.

The collection was configured to refresh the token periodically, approximately every 14 minutes, so subsequent Manager API requests could continue using an up to date token.

### Wazuh Indexer API

Indexer requests use HTTP Basic Authentication. The credentials are supplied with the request rather than reusing the Manager API token.

Credentials and token values are intentionally excluded from this documentation and must not be committed in screenshots or exported collections.

## Requests tested

### Agent information

The Manager API was queried to retrieve the registered agents. The response included the Wazuh manager and the Ubuntu lab endpoint.

### Software inventory

The Manager API Syscollector interface was used to retrieve package inventory for an endpoint. Syscollector provides collected host inventory data, including installed software.

### Alert search

A request was sent to the Indexer API to search the `wazuh-alerts-4.x-*` index pattern. The query used OpenSearch search syntax and returned alert records across the indexed date range covered by the request.

The Indexer stores alert data in indices, with shards used to organise and distribute index data. The exact results depend on the query and the data retained in the lab.

## Results

| Test | Observed result |
|---|---|
| Manager authentication | HTTP 200 and token returned |
| Agent listing | Agent records retrieved |
| Software inventory | Syscollector package data retrieved |
| Alert search | Alert records returned from the Wazuh alert indices |
| Token handling | Postman script stores and refreshes the Manager API token |

These checks establish that Postman can communicate with both Wazuh APIs using their respective authentication methods. They provide the API access pattern needed for the n8n integration.

## Why this stage matters

The previous stage focused on generating and collecting endpoint telemetry. This stage establishes how another application can retrieve Wazuh agent information, software inventory and alert records.

That is the bridge to the next stage: connecting n8n and an AI agent to Wazuh so the agent can work with security data through API requests.

## Evidence

Screenshots for this stage will be added under [`screenshots/03-wazuh-api-postman/`](../../screenshots/03-wazuh-api-postman/) after review.

Planned evidence includes:

1. Postman environment and collection structure with secrets hidden.
2. Successful Manager API authentication response with the token redacted.
3. Agent listing or Syscollector inventory response.
4. Indexer alert search request and response.
5. Token refresh or another representative successful API request.

## Security notes

1. Do not publish usernames and passwords, bearer tokens, API keys or Postman environment exports containing secrets.
2. Redact authentication headers and token values in screenshots.
3. Keep example requests reproducible without exposing the lab's credentials.

## Next stage

[Stage 04: AI cybersecurity agent](lesson-04-ai-cybersecurity-agent.md)
