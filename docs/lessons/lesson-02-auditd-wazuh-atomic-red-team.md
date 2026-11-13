# Stage 02: Auditd, Wazuh and Atomic Red Team

<sup>Status: In progress</sup>

**Masterclass reference:** Lesson 2, *Auditd + Wazuh Integration on Ubuntu | Atomic Red Team Lab*

## Objective

Extend endpoint visibility on Ubuntu with Auditd, collect its audit log through Wazuh and generate controlled activity with Atomic Red Team. This provides endpoint telemetry for the AI-assisted investigation workflows developed in later stages.

## Implementation

### Auditd and Wazuh

Auditd was installed and enabled on the Ubuntu endpoint. The Wazuh agent configuration was updated to collect:

```text
/var/log/audit/audit.log
```

The agent was restarted and its service status checked. The screenshot below records the Wazuh agent running successfully after the configuration change.

![Wazuh agent restarted and confirmed active](../../screenshots/02-auditd-atomic-red-team/01-configuring%20wazuh%20agent%20p2.png)

### Atomic Red Team

Atomic Red Team was installed under `/opt/atomic-red-team`. A Git clone attempt failed during transfer, so the installation was completed using an archive instead. The collection contained 354 Atomic tests.

The first test invocation exposed an incorrect or unavailable atomics path. The command was corrected to use:

```text
/opt/atomic-red-team/atomics
```

The corrected invocation reached the confirmation prompt for the test run.

![Atomic Red Team installation attempt and initial path issue](../../screenshots/02-auditd-atomic-red-team/02-atomic%20red%20team%20deployment%20p2.png)

![Atomic Red Team invocation using the corrected atomics path](../../screenshots/02-auditd-atomic-red-team/03-atomic%20red%20team%20execute%20p2.png)

## Telemetry flow

```text
Ubuntu endpoint activity
        |
        v
Linux Audit Framework
        |
        v
Auditd log
/var/log/audit/audit.log
        |
        v
Wazuh Agent
        |
        v
Wazuh Manager
        |
        v
Wazuh alerts for review
```

## Observed results

The Wazuh Overview dashboard showed the following alert distribution for its last-24-hours view:

| Severity | Alerts |
|---|---:|
| Medium | 184 |
| Low | 213 |
| High | 0 |
| Critical | 0 |
| **Total** | **397** |

![Wazuh Overview showing alert severity counts](../../screenshots/02-auditd-atomic-red-team/04-wazuh%20alerts%20dashboard%20p2.png)

This is the observed dashboard snapshot from this lab, not the instructor's demonstration counts. The dashboard also showed one active and one disconnected agent in its agent summary. These figures are a point-in-time view and should not be interpreted as proof that every Atomic test generated a corresponding alert.

## Why this stage matters

Auditd adds Linux audit records to the endpoint telemetry available to Wazuh. Atomic Red Team provides controlled activity that can be used to examine the events collected and how Wazuh classifies them.

This creates a practical source of endpoint security data for the API integration and AI agent stages that follow.

## Test context

Atomic Red Team testing was performed in the isolated lab. Record specific Atomic test identifiers and any custom Auditd or Wazuh rules when adding deeper test evidence.

## Next stage

[Stage 03: Wazuh API and Postman](lesson-03-wazuh-api-postman.md)
