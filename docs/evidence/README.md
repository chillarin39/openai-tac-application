# Phase 0 Lab Verification Evidence

This directory contains verification logs supporting the **Authorized Target Environment** claim in the [TAC Application Profile](../tac-application-profile.en.md) §4 and §5.

All evidence was captured against the live lab on **2026-05-29** after `terraform apply` provisioned VMID 701 (`kali-edu`) and VMID 702 (`vuln-web-lab`) on Proxmox node `nuc2`.

## Files

| File | What it shows | Why it matters |
|------|--------------|----------------|
| [`2026-05-29-iptables-output.txt`](./2026-05-29-iptables-output.txt) | `sudo iptables -L OUTPUT -n -v` on `kali-edu` | Layer 2 of the 4-layer enforcement (network-layer DROP for NEW connections destined to home production segments `172.16.0.0/12`, `192.168.0.0/16`, `10.1.0.0/16`). The lab-side segment `10.20.0.0/16` is explicitly ACCEPTed. |
| [`2026-05-29-unreachability-prod.txt`](./2026-05-29-unreachability-prod.txt) | 3× `ping -c 3 -W 2` from `kali-edu` to home production gateways (`172.16.1.1`, `192.168.1.1`, `10.1.1.1`) | End-to-end demonstration that the lab cannot reach the production segments. All 9 packets dropped (100% packet loss). This is the core TAC application claim. |
| [`2026-05-29-lab-reachability.txt`](./2026-05-29-lab-reachability.txt) | `ip -br addr`, `ip route`, and the relevant `iptables` ACCEPT line on `kali-edu` | Demonstrates the lab side is correctly configured on `vmbr2 / 10.20.0.0/16` with default route via `10.20.0.1` and that lab-internal traffic is explicitly permitted. (Direct `ping` against `vuln-web-lab` is recorded as failing in this snapshot because VMID 702 hit a boot-time kernel panic and will be re-provisioned separately; the kali-side configuration that the TAC application relies on is independently verifiable here.) |
| [`2026-05-29-no-external.txt`](./2026-05-29-no-external.txt) | `ping -c 3` to `8.8.8.8` and `curl` to `https://example.com` from `kali-edu` | The lab segment has **no Internet egress** at this point in Phase 0, because the default-route placeholder router (VMID 705 `lab-router`) has not yet been deployed. All external probes time out at the IP layer. This is the strongest form of isolation and supports the application’s "no ad-hoc external traffic" claim. |

## Test method

All commands were executed from the WSL2 administrative workstation via the standard SSH access path (`pve2` ProxyJump → `kali-edu`). No production credentials were entered into any AI service during the test. The capture commands and timing are reproducible from [`security-lab.tf`](../../../terraform/security-lab.tf) (in the local Terraform tree) by anyone with the same infrastructure setup.

## Out-of-scope / known issues recorded for transparency

- **VMID 702 (`vuln-web-lab`) boot failure**: at the time of these captures, the Debian 12 genericcloud image used for VMID 702 was hitting an early kernel panic. Because the TAC application's core claim is the *non-reachability of production from kali-edu*, this does not invalidate the evidence in this directory, but it is documented here for completeness. A re-provisioning attempt will produce a follow-up reachability log.
- **Default route placeholder**: the `kali-edu` default route currently points to `10.20.0.1`, a placeholder address that will become VMID 705 (`lab-router`) in a later Phase. Today, that absence is what produces the `no-external` result above. Once VMID 705 is deployed (controlled egress only, with logging), an updated `no-external` log will be added to document the new posture.

## Sanity check before commit

The files in this directory contain only:
- Lab-side IPs (`10.20.10.10`, `10.20.20.10`)
- Documentation-style range references in `iptables` rules (`172.16.0.0/12`, `192.168.0.0/16`, `10.1.0.0/16`) — these are the rule definitions, not exposed production IPs
- The `kali-edu` lab management IP `172.16.1.205` (the lab VM's vmbr0 address, not a production service)

No production credentials, no production service hostnames, no real production traffic samples.
