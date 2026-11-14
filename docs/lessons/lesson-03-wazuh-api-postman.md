# Stage 03: Wazuh API and Postman

<sup>Status: In progress</sup>

## Objective

Test how Wazuh data can be accessed programmatically. Postman was used to authenticate with the Wazuh Manager API, inspect endpoint information and query alert data through the Wazuh Indexer API. These are the interfaces the n8n workflows will use in the next stages.

## API architecture

| Component | Address in the lab | Purpose |
|---|---|---|
| Wazuh Manager API | Port `55000` | Manager operations and endpoint information |
| Wazuh Indexer API | Port `9200` | Search and retrieve indexed alert records |
| Postman | Ubuntu lab environment | Send requests and inspect API responses |

The Manager API and Indexer API serve different purposes. The Manager API provides information about managed agents and their inventory. The Indexer API provides search access to stored Wazuh alert data.

## Authentication

### Wazuh Manager API

A POST authentication request was configured in Postman. The authentication flow returned **HTTP 200** and a JSON Web Token. A Postman script stores the returned token for use in later requests.

The collection was configured to refresh the token periodically, approximately every 14 minutes, so subsequent Manager API requests could continue using a current token.

### Wazuh Indexer API

Indexer requests use HTTP Basic Authentication. The credentials are supplied with the request rather than reusing the Manager API token.

## Requests tested

### Agent information

The Manager API was queried to retrieve the registered agents. The response included the Wazuh manager and the Ubuntu lab endpoint.

### Software inventory

The Manager API Syscollector interface was used to retrieve package inventory for agent `007`, the Ubuntu lab endpoint. Syscollector provides collected host inventory data, including installed software.

### Alert search

A request was sent to the Indexer API to search the `wazuh-alerts-4.x-*` index pattern. The query used OpenSearch search syntax and returned alert records from the indices covered by the request.

The Manager API and Indexer API were tested separately with their respective authentication methods.

## Results

| Test | Observed result |
|---|---|
| Manager authentication | HTTP 200 and token returned |
| Agent listing | Agent records retrieved |
| Software inventory | Syscollector package data retrieved for agent `007` |
| Alert search | Alert records returned from the Wazuh alert indices |
| Token handling | Postman script stores and refreshes the Manager API token |

These checks establish that Postman can communicate with both Wazuh APIs. The results provide the API access pattern needed for the n8n integration.

## Evidence

The screenshots below show the Postman collection, request configuration and Manager API responses.

### Postman collection

![Postman collection structure for Wazuh Manager and Indexer APIs](../../screenshots/03-wazuh-api-postman/01-Postman%20wazuh%20ingest%20and%20setup.png)

The collection separates Manager API operations from Indexer API requests.

### Manager API authentication request

![Postman Manager API authentication request configuration](../../screenshots/03-wazuh-api-postman/01.-Postman%20wazuh%20ingest%20and%20setup.png)

Shows the authentication request setup. The successful HTTP 200 response is recorded in the results above.

### Postman environment

![Postman environment configuration](../../screenshots/03-wazuh-api-postman/02-configuring%20API%20environment%20copy.png)

Shows the Manager and Indexer environment variables used by the collection.

### Agent listing

![Wazuh Manager API agent listing response](../../screenshots/03-wazuh-api-postman/03%20Testing%20management%20APIs.png)

The Manager API returned the registered agent records.

### Syscollector package inventory

![Wazuh Syscollector package inventory for agent 007](../../screenshots/03-wazuh-api-postman/04%20testing%20management%20api%20part%202.png)

The request retrieved package inventory from the Ubuntu endpoint, agent `007`.

The Indexer alert search was also tested, although a response screenshot is not included in this evidence set.

## Why this stage matters

Stage 02 focused on generating and collecting endpoint telemetry. This stage establishes how another application can retrieve Wazuh agent information, software inventory and alert records through APIs.

That is the bridge to Stage 04: connecting n8n and an AI agent to Wazuh so the workflow can retrieve and analyse security data.

## Next stage

[Stage 04: AI cybersecurity agent](lesson-04-ai-cybersecurity-agent.md)
