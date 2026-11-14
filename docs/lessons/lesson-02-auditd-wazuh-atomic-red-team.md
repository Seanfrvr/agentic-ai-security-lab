# Stage 02: Auditd, Wazuh and Atomic Red Team

<sup>Status: Complete</sup>

## Objective

Extend Linux endpoint visibility by collecting Auditd records with Wazuh and generating controlled activity with Atomic Red Team. This provides endpoint data that can be reviewed in Wazuh and queried by the automation workflows built later in the lab.

## Auditd and Wazuh configuration

Auditd was installed and enabled on the Ubuntu endpoint. It records security relevant activity on the host, providing an additional source of operating system telemetry.

The Wazuh agent was configured to monitor the Auditd log:

```text
/var/log/audit/audit.log
```

After updating the agent configuration, the service was restarted and checked to confirm that it was running with the change applied.

![Wazuh agent restarted and confirmed active](../../screenshots/02-auditd-atomic-red-team/01-configuring%20wazuh%20agent%20p2.png)

## Atomic Red Team setup and testing

Atomic Red Team was installed under `/opt/atomic-red-team`. A Git clone attempt failed during transfer, so the repository archive was used instead. The downloaded collection contained 354 Atomic tests.

The initial test invocation referenced an incorrect atomics directory. The path was corrected to:

```text
/opt/atomic-red-team/atomics
```

Atomic tests were then used to generate controlled activity on the Ubuntu endpoint. This provides repeatable test activity that can be examined in the audit records and Wazuh alerts, rather than relying only on naturally occurring system events.

![Atomic Red Team installation](../../screenshots/02-auditd-atomic-red-team/02-atomic%20red%20team%20deployment%20p2.png)

![Atomic Red Team test invocation](../../screenshots/02-auditd-atomic-red-team/03-atomic%20red%20team%20execute%20p2.png)

## Telemetry flow

The configured collection path is:

```text
Ubuntu endpoint activity
        |
        v
Linux Audit Framework
        |
        v
/var/log/audit/audit.log
        |
        v
Wazuh Agent
        |
        v
Wazuh Manager
        |
        v
Wazuh alerts
        |
        v
Analyst review and API queries
```

Auditd provides the endpoint audit records, while the Wazuh agent forwards the configured log to the manager for processing. Wazuh applies its decoders and rules to the collected data and makes generated alerts available for review and API retrieval.

## Observed results

The Wazuh Overview dashboard showed 397 alerts in its last 24 hour view:

| Severity | Alerts |
|---|---:|
| Medium | 184 |
| Low | 213 |
| High | 0 |
| Critical | 0 |
| **Total** | **397** |

![Wazuh alert severity counts](../../screenshots/02-auditd-atomic-red-team/04-wazuh%20alerts%20dashboard%20p2.png)

These figures are a point in time snapshot of the dashboard. They represent the alert volume visible during the selected period and should not be treated as a one to one count of Atomic test executions.

## Outcome

Auditd was configured as an additional source of Linux endpoint telemetry, the Wazuh agent was set to collect its log, and Atomic Red Team was installed and used to generate controlled activity. The resulting Wazuh data provides material for the API queries, alert analysis and AI assisted triage developed in the later stages.

## Next stage

[Stage 03: Wazuh API and Postman](lesson-03-wazuh-api-postman.md)
