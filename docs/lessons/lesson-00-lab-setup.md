# 00. Lab setup

<sup>Status: In progress</sup>

## Objective

Prepare the local Ubuntu environment for the rest of the lab. The environment runs Wazuh and n8n in Docker containers connected through a shared Docker network.

## Environment

| Item | Actual value |
|---|---|
| Host machine | MacBook Pro (Late 2013) |
| Virtualisation software | VirtualBox |
| Lab operating system | Ubuntu Desktop VM |
| Docker version | 29.9.3 |
| Wazuh version | 4.9.0 |
| n8n image | `n8nio/n8n` (tag not pinned in the Compose file) |
| Shared Docker network | `soc-net` |

Ubuntu version and VM resource allocations have not yet been recorded.

## Components

| Component | Role |
|---|---|
| Wazuh Manager | Receives and analyses endpoint data |
| Wazuh Indexer | Stores and indexes security events |
| Wazuh Dashboard | Interface for reviewing alerts and events |
| n8n | Workflow automation |
| `soc-net` | Shared Docker network used by Wazuh and n8n |

## Build record

The Docker daemon initially failed to start because its systemd socket activation unit was in a failed state. The socket and service were recovered with:

```bash
sudo systemctl daemon-reload
sudo systemctl reset-failed docker.socket docker.service
sudo systemctl restart docker.socket
sudo systemctl start docker
```

The existing Wazuh deployment was already present and used version 4.9.0. Its three containers were preserved:

| Container | Image | Observed state |
|---|---|---|
| Wazuh Manager | `wazuh/wazuh-manager:4.9.0` | Running |
| Wazuh Indexer | `wazuh/wazuh-indexer:4.9.0` | Running |
| Wazuh Dashboard | `wazuh/wazuh-dashboard:4.9.0` | Running |

The available startup script targeted Wazuh 4.12.0 and checked for container names that did not match the existing 4.9.0 deployment. It was not run, avoiding an unintended second Wazuh deployment.

The n8n Compose file declared an external network named `soc-net`. That network did not initially exist, so it was created and the three existing Wazuh containers were connected to it. n8n was then started from the local `n8n-docker/docker-compose.yml`.

The resulting `docker ps` output showed four running containers: Wazuh Manager, Indexer, Dashboard and n8n.

## Verification

| Check | Result |
|---|---|
| Ubuntu VM starts | Verified |
| Docker installed | Verified, version 29.9.3 |
| Docker daemon running | Verified after systemd socket recovery |
| Wazuh Manager, Indexer and Dashboard running | Verified |
| Wazuh Dashboard accessible | Verified; dashboard and Agents Management pages opened |
| n8n container running | Verified |
| n8n initial owner setup | Completed |
| Wazuh containers connected to `soc-net` | Verified with `docker network inspect soc-net` |
| n8n to Wazuh application/API communication | Not yet tested |
| Endpoint telemetry from a newly enrolled agent | Not yet tested |

The Wazuh Agents Management page currently lists an older Windows 11 agent named `win11-victim` as disconnected. It has been left registered because it does not prevent this lab from proceeding. No new Ubuntu agent has been enrolled yet.

## Evidence

The following screenshots were captured locally and are ready to be added to the repository.

| Filename | What it demonstrates |
|---|---|
| `01-docker-four-containers.png` | Four running containers: Wazuh Manager, Indexer, Dashboard and n8n |
| `02-wazuh-agent-management.png` | Wazuh Agents Management and the Deploy new agent option |
| `03-n8n-owner-setup.png` | Initial n8n owner account setup |

Once uploaded to `screenshots/00-lab-setup/`, embed each image here so it appears directly in the page.

## Issues and fixes

| Issue | Action |
|---|---|
| Docker daemon unavailable | Recovered the systemd Docker socket and started Docker |
| Existing Wazuh deployment did not match the startup script's expected version and container names | Preserved the existing 4.9.0 containers and avoided running the script |
| n8n expected an external `soc-net` network that did not exist | Created `soc-net` and connected the existing Wazuh containers |
| Existing Windows agent appeared disconnected | Left the old registration in place; it is not required to start the lab |

## Outstanding work

- Verify n8n can authenticate to and query the Wazuh API.
- Record the Ubuntu version and VM resource allocations.
- Pin the n8n image to a deliberate version before relying on repeatable rebuilds.
- Enrol a Linux endpoint when beginning the endpoint telemetry exercises.

## Outcome

The four main containers are running and the local interfaces have been accessed. Stage 00 remains in progress until application-level communication between n8n and Wazuh is tested.

## Next stage

[Stage 01: Wazuh and n8n architecture](lesson-01-wazuh-n8n-architecture.md)
