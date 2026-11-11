# AI-Assisted Enterprise Home Network Virtual Lab

Status: Lab-validated virtual mirror with sanitized public evidence

## Why I started this project

I wanted a safe way to learn how identity, DNS, routing, segmentation, certificate-based access decisions, and deployment services fit together instead of treating each topic as a separate tutorial.

I defined the architecture, device roles, learning goals, isolation rules, evidence requirements, and stopping conditions. I then directed an AI-assisted implementation and reviewed the resulting configurations, failures, corrections, screenshots, hashes, and validation records before accepting each stage.

I use AI to speed up research, documentation, testing, and project work while keeping validation and final decisions in my hands.

This is not a claim that I configured every component from memory. It is a documented learning environment that shows how I define requirements, control risk, review evidence, troubleshoot failures, and separate a lab result from a production claim.

## What the lab demonstrates

The lab is an isolated enterprise-style network built on Hyper-V. It covers Windows Server identity and DNS, Group Policy, Windows LAPS, OPNsense routing and segmentation, FreeRADIUS EAP-TLS decisions, persistent approved and quarantined clients, and a diskless PXE service-response test.

Every lab switch uses Hyper-V Private networking. The environment does not connect to or replace the household router, DHCP, DNS, firewall, Wi-Fi, or physical network.

## Lab-validated architecture

```mermaid
flowchart LR
    M[Management99] --> OPN[OPNsense 26.7]
    M --> RAD[FreeRADIUS and lab CA]
    OPN --> T[Trusted10]
    OPN --> I[IoT20]
    OPN --> G[Guest30]
    OPN --> Q[Quarantine40]
    OPN --> D[Deployment50]
    OPN --> U[Isolated upstream]

    T --> DC[DC1: AD and DNS]
    T --> WIN[Windows domain client]
    T --> APP[Approved Linux client]
    Q --> UNKNOWN[Unknown Linux client]
    D --> PXE[PXE1 and diskless UEFI target]
    RAD -. EAP-TLS accept, VLAN 10, reject .-> APP
```

## Verified results

| Area | Result |
|---|---|
| Recovery | Hash-verified local backup and sample restore preserved |
| Hyper-V isolation | Seven Private lab switches, no physical binding, host adapter, or lab NAT |
| Active Directory | Private AD domain, DNS, domain client, OU/user/group/GPO/LAPS workflow tested |
| OPNsense | Six segment gateways plus isolated upstream installed and running |
| Segmentation | Trusted allow; IoT, Guest, and Quarantine denies; narrow Deployment DNS path |
| FreeRADIUS | Local accept/reject, EAP-TLS accept, VLAN 10 response, and untrusted-certificate reject |
| Test clients | Persistent approved and unknown Alpine clients installed and validated |
| PXE | DHCP lease and WDS service response to a diskless UEFI target |

## Important claim boundary

This project supports claims about requirements definition, directed AI-assisted implementation, evidence review, troubleshooting, and validation of a virtual network design. It does not prove independent production administration, physical 802.1X, MAB, dynamic VLAN enforcement, household-network deployment, or Windows image deployment.

## Workflow

1. Verify backup and recovery.
2. Inventory the host and record risks.
3. Build private virtual switches.
4. Build AD, DNS, client identity, and policy.
5. Install OPNsense and apply default-deny segmentation.
6. Install FreeRADIUS and the lab certificate authority.
7. Prove EAP-TLS accept and reject results.
8. Install approved and unknown endpoints and test the allow or block paths.
9. Preserve the safe diskless PXE service-response boundary.
10. Separate private evidence from public claims and document what remains physical work.

## What failed and what I learned

The project kept failed results instead of writing around them:

- A correct Deployment rule still failed until the return route and DNS-specific endpoint firewall scope were reviewed together. This reinforced that routing must work in both directions.
- The first diskless PXE attempt received no lease because DHCP authorization was incomplete. The service path passed only after that dependency was corrected and the original test was repeated.
- The approved and unknown Linux clients booted from their installed disks, but their live-session network settings had not carried into the installed systems. Post-install validation caught the difference before the result was accepted.
- FreeRADIUS could return an accept, reject, and network-role response, but a physical switch or access point would still need to enforce that decision. A policy decision is not the same as physical network access control.

These failures are part of the project because they show how I review a result, narrow the cause, apply one correction, and repeat the original test.

## How I review the evidence

I keep each claim tied to a positive test, a denied or negative test when appropriate, and an explicit limit:

- Isolation checks cover private-switch type, physical binding, host access, and NAT exposure.
- Segmentation checks cover an approved path and denied IoT, Guest, and Quarantine paths.
- EAP-TLS checks cover an approved certificate, returned network role, and untrusted-certificate rejection.
- Persistent-client checks cover the installed system after reboot, not only the temporary live environment.
- PXE checks cover the DHCP and WDS service response while preserving the boundary that no operating system was deployed.

## Public evidence boundary

This public README was derived from a 25-file, hash-verified local package. The full package remains private because it contains detailed lab addressing, host and domain identifiers, build procedures, and screenshots that are useful for local evidence but unnecessary for a public portfolio.

Credentials, private keys, shared secrets, household addresses, recovery data, raw logs, private configuration exports, full machine inventories, and unrelated personal information are not published.

