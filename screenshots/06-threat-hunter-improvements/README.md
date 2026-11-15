# Stage 06 evidence

Nine screenshots document the host threat hunting review, vulnerable web application deployment, controlled command execution and Wazuh archive validation.

## Evidence gallery

### Host threat hunting

The first two screenshots show Wazuh Dashboard Events filtered to agent `007` and audit related activity. The expanded event details include the audit rule description, rule ID and severity.

![Host audit event details](01-%20threat%20hunting.png)

![Host audit rule metadata](01-threat%20hunting%202.png)

### Vulnerable application deployment

The deployment screenshot records the Docker run configuration, including resource limits, port mapping, read-only application mount and the `no-new-privileges` option.

**Publication note:** the original deployment screenshot exposes a full Docker container ID. Replace it with a redacted image before promoting this evidence as publication-ready.

### Application and command execution

The web application is shown running locally with a diagnostic command field. The following two screenshots show the observed command output from tests inside the container.

![Vulnerable web application](03-vulnerable%20website.png)

![whoami command output](04-whoamii%20test.png)

![id command output](05-id%20testing%20vuln%20web.png)

The outputs identify the execution account as `www-data`. The `id` output also shows UID 33 and GID 33. This confirms the commands ran as the web server account inside the container, not as the Ubuntu host user.

### Wazuh archive data view and event validation

The index pattern creation screenshot shows `wazuh-archives-*` matching the archive index.

![Wazuh archives index pattern](06-index%20pattern%20creation.png)

The Discover screenshot shows a search for `whoami` returning four matching documents in the selected time range. The detailed event view below identifies the Apache GET request, agent `007`, decoder `json`, stdout stream and HTTP status `200`.

![whoami archive search results](07-whoami%20cmd%20discovery.png)

![Detailed archived Apache request](08-cmd%20whoami%20log%20details%20.png)

## What the evidence establishes

- Host audit events were available for review in Wazuh Dashboard Events.
- The vulnerable PHP and Apache application ran in a Docker container with resource and privilege restrictions.
- The `whoami` and `id` tests executed as `www-data` inside the application container.
- The Apache request for `whoami` was collected by Wazuh Agent `007`.
- The request was searchable in the Wazuh archives data view.

The archived web request is raw telemetry, not a Wazuh alert. This stage does not claim that a custom detection rule or automated response was implemented.

## Evidence hygiene

Before sharing the repository publicly, replace the original deployment screenshot with a redacted version that hides the full Docker container ID. Review all images for credentials, tokens, private configuration and personal host details.

## Related documentation

See [Stage 06: Threat hunter lab improvements](../../docs/lessons/lesson-06-threat-hunter-lab-improvements.md) for the build details, validation steps and current limitations.
