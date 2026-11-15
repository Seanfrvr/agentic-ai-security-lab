# Stage 06: Threat hunter lab improvements

Screenshots documenting host audit investigation, deployment of the vulnerable web application, controlled command execution and validation of Wazuh archive collection.

## Host threat hunting

| Screenshot | Evidence |
|---|---|
| [01 Threat hunting](01-%20threat%20hunting.png) | Wazuh Dashboard Events showing host audit activity associated with agent 007. |
| [01 Threat hunting 2](01-threat%20hunting%202.png) | Expanded audit event details, including the rule metadata for promiscuous mode activity. |

## Vulnerable web application

| Screenshot | Evidence |
|---|---|
| [02 Vulnerable site deployment](02-vulnerable%20site%20deployment%20.png) | Docker deployment command showing the container resource limits, port mapping, read-only application mount and no-new-privileges setting. |
| [03 Vulnerable website](03-vulnerable%20website.png) | PHP and Apache application running locally in the browser. |
| [04 whoami test](04-whoamii%20test.png) | Command injection test returning the web server account, www-data. |
| [05 id testing](05-id%20testing%20vuln%20web.png) | User and group identity output confirming UID 33 and GID 33 inside the container. |

## Wazuh archive validation

| Screenshot | Evidence |
|---|---|
| [06 Index pattern creation](06-index%20pattern%20creation.png) | Creation of the wazuh-archives-* data view using timestamp as the time field. |
| [07 whoami command discovery](07-whoami%20cmd%20discovery.png) | Discover search results for the whoami request in the Wazuh archives index. |
| [08 whoami log details](08-cmd%20whoami%20log%20details%20.png) | Expanded archive event showing the Apache request, agent metadata and JSON decoder. |

The detailed implementation, validation sequence and limitations are documented in [Stage 06](../../docs/lessons/lesson-06-threat-hunter-lab-improvements.md).
