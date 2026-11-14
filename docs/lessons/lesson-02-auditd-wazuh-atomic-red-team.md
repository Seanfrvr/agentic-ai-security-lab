# Stage 02: Auditd, Wazuh and Atomic Red Team

<sup>Status: Complete</sup>

## Objective

Configure Linux audit collection with Auditd, forward the audit log through Wazuh and generate controlled endpoint activity with Atomic Red Team.

## Implementation

Auditd was installed and enabled on the Ubuntu endpoint. The Wazuh agent was configured to monitor:

```text
/var/log/audit/audit.log
```

The agent was restarted and confirmed active.

![Wazuh agent restarted and confirmed active](../../screenshots/02-auditd-atomic-red-team/01-configuring%20wazuh%20agent%20p2.png)

Atomic Red Team was installed under `/opt/atomic-red-team`. After a Git clone failed during transfer, the collection was installed from an archive. The installation contained 354 Atomic tests.

The atomics path was corrected to:

```text
/opt/atomic-red-team/atomics
```

![Atomic Red Team installation](../../screenshots/02-auditd-atomic-red-team/02-atomic%20red%20team%20deployment%20p2.png)

![Atomic Red Team test invocation](../../screenshots/02-auditd-atomic-red-team/03-atomic%20red%20team%20execute%20p2.png)

## Telemetry flow

```text
Ubuntu activity
      |
    Auditd
      |
audit.log
      |
 Wazuh Agent
      |
 Wazuh Manager
      |
 Wazuh alerts
```

## Results

The Wazuh Overview dashboard showed 397 alerts in its last 24 hours view:

| Severity | Alerts |
|---|---:|
| Medium | 184 |
| Low | 213 |
| High | 0 |
| Critical | 0 |
| **Total** | **397** |

![Wazuh alert severity counts](../../screenshots/02-auditd-atomic-red-team/04-wazuh%20alerts%20dashboard%20p2.png)

This is a point in time dashboard snapshot. It does not establish that every Atomic test generated a corresponding alert.

## Outcome

Auditd log collection was configured through the Wazuh agent, and Atomic Red Team was installed for controlled endpoint testing. The resulting Wazuh alert data provided telemetry for subsequent investigation and automation stages.

## Next stage

[Stage 03: Wazuh API and Postman](lesson-03-wazuh-api-postman.md)
