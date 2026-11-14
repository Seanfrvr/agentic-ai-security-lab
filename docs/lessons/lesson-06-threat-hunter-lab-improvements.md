# Stage 06: Threat hunter lab improvements

<sup>Status: In progress</sup>

## Objective

Extend the local lab with a controlled vulnerable web application and verify that its activity can be collected and searched as raw telemetry in Wazuh. This provides a source of web activity for later detection engineering and investigation.

## Environment

The existing Ubuntu 22.04 virtual machine hosts Wazuh, n8n and the vulnerable web application. The application runs in its own Docker container rather than requiring another virtual machine.

| Component | Role |
|---|---|
| Ubuntu 22.04 | Local lab host |
| Docker | Runs the web application alongside the security stack |
| PHP 8.2 and Apache | Hosts the deliberately vulnerable application |
| Wazuh Agent 007 | Collects the Docker container log |
| Wazuh Manager | Receives and processes collected log data |
| Filebeat | Forwards archive data to the Indexer |
| Wazuh Indexer | Stores searchable archive events |
| Wazuh Dashboard | Provides Discover for reviewing events |

The application is accessible from the host browser through the VirtualBox forwarded port at `http://localhost:8088`.

## Vulnerable web application

A PHP and Apache application was deployed in a Docker container named `vulnerable-web`. It accepts a diagnostic command through a GET parameter and intentionally passes the supplied value to a system command. This creates a controlled command injection test point.

The container has resource limits to reduce its impact on the resource-constrained virtual machine. Testing for this validation was limited to the harmless `whoami` command. The application is deliberately vulnerable and must remain a lab-only target, not exposed to an untrusted network.

## Telemetry collection

Apache request activity is written to the container's standard output and retained in Docker's JSON log. The Wazuh agent on the Ubuntu host was configured to collect this log.

JSON archive logging was enabled in the Wazuh Manager configuration:

```xml
<logall>no</logall>
<logall_json>yes</logall_json>
```

The Filebeat Wazuh archives fileset was enabled while retaining the alerts fileset. The Filebeat configuration was validated successfully and reported `Config OK`.

This configuration retains searchable event data. An archived event is not automatically a Wazuh alert.

## Validation

A harmless `whoami` request was submitted through the web application. The request appeared in the Docker log and was collected by Wazuh Agent 007, identified as `ubuntu-local`. Filebeat forwarded the event and it was indexed in the Wazuh archives index.

A `wazuh-archives-*` data view was created in Wazuh Dashboards, using `timestamp` as its time field. Searching for `whoami` returned the archived web request in Discover.

| Field | Verified value |
|---|---|
| Agent name | `ubuntu-local` |
| Agent ID | `007` |
| Decoder | `json` |
| Log stream | `stdout` |
| HTTP request | `GET /index.php?cmd=whoami` |
| HTTP response | `200` |
| Data view | `wazuh-archives-*` |

The verified data path:

```text
Host browser
  -> Vulnerable PHP application
  -> Docker JSON log
  -> Wazuh Agent 007
  -> Wazuh Manager
  -> Filebeat
  -> Wazuh Indexer archives
  -> Wazuh Dashboard Discover
```

## Findings and limitations

- The web request was captured and indexed as raw archive data.
- This event was not a Wazuh alert. No detection rule was created during this validation.
- Only the harmless `whoami` request was used for this validation. Further reconnaissance commands are deferred to the next phase.
- Windows and Kali telemetry are not part of this verified test. The current validation uses the Ubuntu VM and Docker hosted web application.
- Detection logic and alert generation remain separate tasks.
- Screenshots will be added after transfer and review.

## Security and evidence handling

The application is intentionally vulnerable and is intended only for controlled lab testing. Keep it off public networks.

Before publishing screenshots or logs, review them for credentials, tokens, private configuration, host paths and full Docker container identifiers. Do not commit secrets or sensitive environment files.

## Outcome

The vulnerable web application is running in Docker, and its `whoami` HTTP request has been traced from the application log through Wazuh collection into the searchable OpenSearch archive index.

The current telemetry validation is complete. Stage 06 remains in progress while broader lab improvements are developed and verified.

## Next work

Build on this telemetry with additional controlled activity, detection development and event investigation. Windows and Kali integration can be revisited when VM resources allow.

## Evidence

Screenshots for this stage are pending transfer and review. See the [Stage 06 evidence notes](../../screenshots/06-threat-hunter-improvements/README.md).
