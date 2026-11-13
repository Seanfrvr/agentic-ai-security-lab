# Stage 02: Auditd, Wazuh and Atomic Red Team

<sup>Status: In progress</sup>

**Masterclass reference:** Lesson 2, *Auditd + Wazuh Integration on Ubuntu | Atomic Red Team Lab*

## Objective

Add Linux audit telemetry to the Ubuntu endpoint, collect it through Wazuh and generate controlled endpoint activity with Atomic Red Team. This establishes a richer source of endpoint events for the AI-assisted investigation workflows built in later stages.

## Lab implementation

### Auditd and Wazuh

Auditd was installed and enabled on the Ubuntu endpoint. The Wazuh agent was configured to collect the Auditd log at:

```text
/var/log/audit/audit.log
```

The collection path connects Linux audit records with the existing Wazuh monitoring stack. The Ubuntu endpoint appeared in Wazuh as agent `007` (`ubuntu-local`) and was active during the lab checks.

### Atomic Red Team

Atomic Red Team was installed under:

```text
/opt/atomic-red-team
```

The repository was obtained using a release archive after the normal Git clone attempt failed. The installed collection contained 354 Atomic tests.

Tests were run against the isolated Ubuntu lab to generate endpoint activity for Wazuh to collect. The tests provide controlled examples of ATT&CK-related behaviour; the presence of an alert alone does not establish that every simulated technique was detected or that a real compromise occurred.

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
Wazuh Agent (ubuntu-local, agent 007)
        |
        v
Wazuh Manager
        |
        v
Wazuh alerts for analyst review
```

## Observed results

Following the Atomic Red Team testing, the Wazuh alert view showed this severity distribution:

| Severity | Alerts observed |
|---|---:|
| Medium | 184 |
| Low | 213 |
| High | 0 |
| Critical | 0 |
| **Total** | **397** |

This is the observed alert snapshot from the user's lab, not the instructor's demonstration counts. No high or critical alerts appeared in this snapshot. The result provides a baseline for later work on rule coverage and alert quality; it does not by itself mean the simulated activity was harmless or that all relevant behaviour was detected.

## Why this stage matters

The lab now has an additional endpoint telemetry source beyond the default event collection. Atomic Red Team provides repeatable activity that can be used to examine what Wazuh records and how its rules classify that activity.

This gives the later n8n and AI agent stages security events to retrieve, summarise and investigate rather than relying on synthetic example alerts.

## Evidence

Screenshots for this stage will be added under [`screenshots/02-auditd-atomic-red-team/`](../../screenshots/02-auditd-atomic-red-team/) after review and sanitisation.

Planned evidence includes:

- Auditd service and log activity on Ubuntu.
- Wazuh agent status for the Ubuntu endpoint.
- Atomic Red Team installation or test execution.
- Wazuh alert results after the test activity.

## Security notes

- Atomic tests were run in the isolated lab environment.
- Review screenshots and terminal output before committing them. Remove credentials, tokens, private configuration and unrelated sensitive host details.
- Keep the exact test identifiers and any custom Auditd or Wazuh rules alongside the evidence when they are captured, so the activity can be reproduced accurately.

## Next stage

[Stage 03: Wazuh API and Postman](lesson-03-wazuh-api-postman.md)
