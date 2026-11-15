# Stage 06: Threat hunter lab improvements

<sup>Status: In progress</sup>

## Objective

Extend the existing security lab to support future attack simulation, endpoint investigation and AI assisted threat hunting. This stage introduces host audit evidence and a controlled vulnerable web application, while establishing the telemetry collection and indexing required to investigate activity through Wazuh.

The environment will serve as a foundation for subsequent attack chain exercises and the development of the AI Threat Hunter Agent.

## Environment

The existing Ubuntu 22.04 virtual machine hosts Wazuh, n8n and the vulnerable web application. The application runs in its own Docker container rather than requiring another virtual machine.

| Component | Role |
|---|---|
| Ubuntu 22.04 | Local lab host |
| Docker | Runs the web application alongside the security stack |
| PHP 8.2 and Apache | Hosts the deliberately vulnerable application |
| Wazuh Agent 007 | Collects host and configured container log data |
| Wazuh Manager | Receives and processes collected log data |
| Filebeat | Forwards archive data to the Indexer |
| Wazuh Indexer | Stores searchable archive events |
| Wazuh Dashboard | Provides threat hunting and Discover views |

The application is accessible from the host browser through the VirtualBox forwarded port at `http://localhost:8088`.

## Host threat hunting

Wazuh Dashboard Events was used to inspect host telemetry associated with agent `007`. The captured audit events describe a network interface entering promiscuous mode and expose the associated audit rule metadata. This is host audit telemetry reviewed during threat hunting, separate from the vulnerable web application tests.

**Host audit event**

![Wazuh host audit event for promiscuous mode activity](../../screenshots/06-threat-hunter-improvements/01-%20threat%20hunting.png)

**Expanded audit event details**

![Expanded Wazuh audit event details](../../screenshots/06-threat-hunter-improvements/01-threat%20hunting%202.png)

## Vulnerable web application

A PHP and Apache application was deployed in a Docker container named `vulnerable-web`. It accepts a diagnostic command through a GET parameter and intentionally passes the supplied value to a system command. This creates a controlled command injection test point.

The container was started with resource constraints, a read-only application mount and the `no-new-privileges` security option. It was published on host port `8088` and accessed locally through the VirtualBox forwarded port.

The application is deliberately vulnerable and must remain a lab-only target, not exposed to an untrusted network.

**Docker deployment**

![Docker deployment of the resource constrained vulnerable web application](../../screenshots/06-threat-hunter-improvements/02-vulnerable%20site%20deployment%20.png)

**Application running locally**

![Vulnerable PHP web application running in the browser](../../screenshots/06-threat-hunter-improvements/03-vulnerable%20website.png)

## Controlled command execution

The application was tested with the following basic commands:

| Command | Observed output | What it demonstrates |
|---|---|---|
| `whoami` | `www-data` | The command ran under the web server account |
| `id` | `uid=33(www-data) gid=33(www-data) groups=33(www-data)` | Confirms the process user and group identity |

These tests confirm that the supplied diagnostic commands execute within the web application container under the unprivileged `www-data` account. They do not demonstrate access to the Ubuntu host.

## Telemetry collection and archive indexing

Apache request activity is written to the container's standard output and retained in Docker's JSON log. The Wazuh agent on the Ubuntu host was configured to collect this log.

JSON archive logging was enabled in the Wazuh Manager configuration:

```xml
<logall>no</logall>
<logall_json>yes</logall_json>
```

The Filebeat Wazuh archives fileset was enabled while retaining the alerts fileset. The Filebeat configuration was validated successfully and reported `Config OK`.

A `wazuh-archives-*` data view was created in Wazuh Dashboards, using `timestamp` as its time field.

**Archive index pattern**

![Wazuh archives index pattern creation](../../screenshots/06-threat-hunter-improvements/06-index%20pattern%20creation.png)

## Validation result

A `whoami` request was submitted through the web application. The matching Apache request was found in the Docker log and then in Wazuh Discover as an archived event.

| Field | Observed value |
|---|---|
| Agent name | `ubuntu-local` |
| Agent ID | `007` |
| Decoder | `json` |
| Log stream | `stdout` |
| HTTP request | `GET /index.php?cmd=whoami` |
| HTTP response | `200` |
| Data view | `wazuh-archives-*` |

The Discover search for `full_log: *whoami*` returned four matching documents in the captured time range. The detailed event view identifies the web request by its Apache access log entry, agent metadata and JSON decoder.

**Discover search results**

![Wazuh Discover search results for the whoami request](../../screenshots/06-threat-hunter-improvements/07-whoami%20cmd%20discovery.png)

**Expanded archive event**

![Expanded Wazuh archive event showing the Apache request details](../../screenshots/06-threat-hunter-improvements/08-cmd%20whoami%20log%20details%20.png)

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

**Important distinction:** the web request was indexed as raw archive data. It was not itself a Wazuh alert, and no custom detection rule was created as part of this validation.

## Findings and limitations

- Host audit telemetry was reviewed in Wazuh Dashboard Events.
- The vulnerable PHP application was deployed in a resource-constrained Docker container.
- The `whoami` and `id` commands executed as `www-data` inside the application container.
- The `whoami` HTTP request was collected and indexed in `wazuh-archives-*`.
- The current validation does not demonstrate Windows or Kali telemetry.
- Detection logic, alert generation and response automation remain separate tasks.

## Outcome

The lab now contains a controlled command injection test application, verified command execution under the web server account, host audit investigation evidence and a confirmed path for the application's Apache request log into searchable Wazuh archive data.

Stage 06 remains in progress while detection development and further investigation are built and validated.

## Evidence

The screenshots are embedded above at the relevant points in the build and validation narrative. The [Stage 06 screenshot folder](../../screenshots/06-threat-hunter-improvements/) contains the complete evidence set.
