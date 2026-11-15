# Stage 07: Endpoint telemetry

<sup>Status: Complete for the current Linux telemetry scope</sup>

## Objective

Prepare the Ubuntu endpoint for security monitoring with Wazuh Agent and Auditd, then verify that host activity reaches Wazuh in a searchable form. Windows and Sysmon coverage are retained as possible future extensions rather than requirements for the current build.

## Environment

The existing Ubuntu 22.04 virtual machine hosts the Wazuh Manager, Indexer, Dashboard, n8n and the local Wazuh Agent.

| Component | Role |
|---|---|
| Ubuntu 22.04 | Lab host and monitored Linux endpoint |
| Wazuh Agent 007 | Collects host and configured log sources |
| Auditd | Records selected process execution and permission change activity |
| Wazuh Manager | Receives and analyses endpoint events |
| Wazuh Indexer | Stores searchable archive events and alerts |
| Wazuh Dashboard | Supports event review and threat hunting |

The Ubuntu host is also the lab orchestrator. For that reason, the exercises did not modify the host Python binary to create a SUID privilege escalation path.

## Auditd configuration and validation

Auditd was enabled and configured with local rules for selected execution and permission modification activity.

The rules covered:

- Execution of the Python interpreter.
- Permission changes through `chmod`, `fchmod` and `fchmodat`.

The rules were loaded with `augenrules` and checked with `auditctl -l`. Controlled tests confirmed that Python execution and a file permission change produced Auditd records.

![Python execution Auditd rule configuration](../../screenshots/07-endpoint-telemetry/01-python%20config.png)

![Auditd event recorded for the Python execution rule](../../screenshots/07-endpoint-telemetry/02-priv%20esaclation.png)

The Auditd log was collected by Wazuh Agent 007. In Wazuh Discover, the event was visible in `wazuh-archives-*` with the Auditd decoder and fields including the event key, executable, command and user identifiers.

## Authentication and system log collection

The agent configuration was updated to collect the existing host log sources:

| Source | Purpose | Validation |
|---|---|---|
| `/var/log/audit/audit.log` | Auditd process and file activity | Confirmed in Wazuh archives |
| `/var/log/auth.log` | Authentication and sudo activity | PAM and sudo events visible |
| `/var/log/syslog` | Host service and system messages | Events visible in Wazuh |

The new entries were placed inside the existing `<ossec_config>` structure. The Wazuh log collector configuration was tested and the agent restarted successfully.

![Authentication events collected from auth.log](../../screenshots/07-endpoint-telemetry/03-auth.log%20event.png)

![System events collected from syslog](../../screenshots/07-endpoint-telemetry/04-syslog%20events.png)

Authentication events included PAM session open and close records and sudo activity. These records provide context for host administration and authentication investigations. They must not be attributed to the Kali attacker unless the event evidence supports that conclusion.

## Findings

- Auditd was active and selected rules were loaded successfully.
- Python execution and permission modification activity were recorded by Auditd.
- Wazuh Agent 007 collected the Auditd log.
- The Auditd decoder parsed events in the Wazuh archives index.
- Authentication and syslog sources were collected and searchable.
- The Ubuntu endpoint now provides host activity that can be correlated with the web application telemetry documented in Stage 08.

## Scope and future expansion

The current implementation focuses on Linux telemetry from the Ubuntu lab host. A Windows endpoint and Sysmon are not part of the verified build. The previously registered Windows agent was disconnected during this work, and no Windows event collection was validated.

Windows event channels and Sysmon can be added later if the lab is expanded with a suitable target machine. This is an extension to the current scope, not a prerequisite for investigating the evidence already collected.

## Outcome

Linux endpoint telemetry is configured and verified across Auditd, authentication and system log sources. The collected events are available in Wazuh for investigation and correlation.

## Next stage

[Stage 08: Attack chain investigation](lesson-08-attack-chain-investigation.md)
