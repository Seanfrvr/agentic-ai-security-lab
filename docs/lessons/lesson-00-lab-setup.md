# 00. Lab setup

<sup>Status: Not started</sup>

## Reference

[Lesson 0: Lab Setup for Agentic AI Security Automation](https://www.youtube.com/watch?v=fgxwkfjNOA8)

[Masterclass playlist](https://www.youtube.com/playlist?list=PLtyp1BBFawaz946JTxU1MOVZE13d37Yp7)

[Instructor's lab setup repository](https://github.com/Atlantium-AI/wazuh-n8n-lab-setup)

## Objective

Prepare the local environment for the rest of the lab. The lesson introduces an Ubuntu virtual machine, Docker, Wazuh, n8n and a custom Docker network called `SockNet`.

This page will be updated with the exact configuration used in my own build.

## Planned components

| Component | Purpose |
|---|---|
| Ubuntu | Host environment for the lab services |
| Docker | Runs the lab services in containers |
| Wazuh Indexer | Stores and indexes security events |
| Wazuh Manager | Receives and analyses endpoint data |
| Wazuh Dashboard | Interface for reviewing alerts and events |
| n8n | Workflow automation |
| SockNet | Docker network for communication between services |
| Git | Retrieves the instructor's setup files |

These are the components covered by the lesson. Their final versions and configuration will be recorded after installation.

## Environment

| Item | Actual value |
|---|---|
| Host operating system | Pending |
| Virtualisation software | Pending |
| Ubuntu version | Pending |
| VM CPU allocation | Pending |
| VM memory allocation | Pending |
| VM disk allocation | Pending |
| Docker version | Pending |
| Wazuh version | Pending |
| n8n version | Pending |

## Setup record

The lesson references installing Git and cloning the instructor's repository.

Commands shown in the lesson transcript:

```bash
sudo apt install git
git clone https://github.com/Atlantium-AI/wazuh-n8n-lab-setup
cd wazuh-n8n-lab-setup
```

I will add the remaining installation commands and configuration after checking them against the actual build. I will not assume that commands from a different version of the setup repository are identical.

## Verification

| Check | Result |
|---|---|
| Ubuntu VM starts correctly | Not tested |
| Docker is installed and running | Not tested |
| Wazuh services start | Not tested |
| n8n is reachable locally | Not tested |
| Containers share the expected network | Not tested |

## Evidence

Screenshots will be added here as the setup is completed.

Suggested evidence:

- Ubuntu VM and system details
- Docker version and running containers
- Wazuh services running
- n8n interface reachable locally
- Docker network showing the lab containers

Do not include passwords, API keys, access tokens or other secrets in screenshots.

## Issues and fixes

Record the exact error, the cause if known, the fix and how the fix was verified.

_No issues recorded yet._

## Outcome

Pending. This stage is complete when the required services are running and their connectivity has been checked.

## Next stage

[Stage 01: Wazuh and n8n architecture](lesson-01-wazuh-n8n-architecture.md)
