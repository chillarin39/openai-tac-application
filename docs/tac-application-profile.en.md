# OpenAI TAC / GPT-5.5 Cyber Access Application Profile

**Applicant Handle**: chillarin39
**Application Type**: Individual
**Target Tier**: Trusted Access for Cyber (TAC), with potential graduation to GPT-5.5 Cyber
**Version**: Draft v1.0
**Last Updated**: 2026-05-29
**Canonical URL**: https://github.com/chillarin39/openai-tac-application/blob/main/docs/tac-application-profile.en.md

> **Note**: This is a public working draft (in English) for the OpenAI TAC application. Replace placeholders (marked `<...>`) with concrete personal information at submission time. The submitted version is kept in the local `docs/submitted/` directory (gitignored) and is not published.

---

## 1. Applicant Summary

I am an independent security researcher and technical author based in Japan, currently writing a 13-chapter / 74-section Japanese-language cybersecurity field guide aimed at intermediate learners. The guide is to be published on my blog at https://chillablog.chillarin39.com/study/security/ and is accompanied by a physically isolated educational lab environment built on a self-hosted Proxmox VE cluster.

My defensive focus is on:
- Hands-on explanation of attacker techniques **paired with** their corresponding defensive controls
- Detection rule authoring (Suricata, Snort, Sigma) verified against intentionally vulnerable targets
- Translating frameworks (MITRE ATT&CK, NIST CSF 2.0, OWASP Top 10) into reproducible lab exercises for Japanese-speaking learners

I am applying for TAC primarily to remove the over-refusal friction that general-purpose ChatGPT exhibits when reviewing offensive concepts that need to be discussed in parallel with their defensive countermeasures within a controlled educational context.

## 2. Relevant Background and Track Record

- **Cybersecurity Educational Lab Guide (in progress)**: 13 chapters, 74 sections, scheduled across 12-18 months
- **Parallel Network Engineering Guide (in progress)**: 8-chapter Cisco IOS-XE / CML 2.9 verified network engineering guide
- **Independent infrastructure**: Self-hosted Proxmox VE cluster (3 nodes), full Infrastructure as Code (Terraform `bpg/proxmox` provider), Ansible automation, observability stack (Grafana / Prometheus / Loki)
- **Open source / public output**: GitHub https://github.com/chillarin39
- **Active blog**: https://chillablog.chillarin39.com/ (technical articles on infrastructure, networking, and security education)
- **Personal Hub**: https://chillarin39.com/

## 3. Defensive Use Case (Specific)

I plan to use TAC for the following clearly defensive tasks:

1. **Educational content authoring**: drafting OWASP Top 10 and MITRE ATT&CK chapter content where attack technique explanation and defense (WAF rule, SIEM detection, secure coding pattern) are written side by side
2. **Detection rule validation**: generating and reviewing Suricata / Snort / Sigma rule candidates, then verifying them against intentionally vulnerable targets (DVWA, Juice Shop, Metasploitable2, vulhub) inside the isolated lab
3. **CVE impact triage**: assessing exposure of specific CVEs against my self-hosted services, planning patch verification steps
4. **Secure code review**: reviewing pull requests in my own repositories for security regressions
5. **Incident response training**: triaging synthetic log datasets (auth.log, Suricata eve.json) and extracting IOCs for tabletop exercises
6. **IaC review**: reviewing Terraform and Ansible playbooks for misconfigurations

## 4. Authorized Target Environment

All AI-assisted execution is constrained to a **physically isolated educational lab segment**:

- **Network segment**: `10.20.0.0/16` on a slaveless internal Linux bridge (`vmbr2`) in Proxmox VE. No layer-2 path to the production segment (`172.16.1.0/24`).
- **Lab VMs** (VMID 701-705, all consolidated on Proxmox node `nuc2`):
  - 701 `kali-edu` — Kali Linux 2026.x, dual-NIC (vmbr0 management + vmbr2 lab), with an iptables `OUTPUT` rule that DROPs new connections destined outside `10.20.0.0/16`
  - 702 `vuln-web-lab` — Debian 12 + Docker, hosting DVWA / Juice Shop / vulhub containers
  - 703 `metasploitable2`
  - 704 `blue-lab` — Ubuntu 22.04 for defender-side exercises
  - 705 `lab-router` — for L2 attack exercises (ARP spoofing, etc.)

> **Status as of 2026-05-29**: the `vmbr2` segment is applied via Terraform across all three Proxmox nodes. VM provisioning (701-705) is in progress as Phase 0 of the lab setup. The TAC application will be submitted **after Phase 0 completion** and verification of the iptables OUTPUT DROP rule and end-to-end unreachability from the lab to the production segment.

**Explicitly out of scope**:
- Home production network (`172.16.1.0/24` Proxmox cluster, `10.1.1.0/24` Cisco network gear, `192.168.1.0/24` NAS)
- Any third-party systems on the public internet
- My personal `redteam-lab` project (which targets the home production network and is therefore **not** within TAC/Cyber scope)

## 5. Enforcement Controls

Defensive scope is enforced both procedurally and technically:

1. **Runtime IP guard**: every PoC script in the lab repository sources `ip_guard.sh`, which rejects any target outside `10.20.0.0/16` at execution time with a clear error message referencing the Japanese Unauthorized Computer Access Act.
2. **Commit-time ethics lint**: `ethics_lint.sh` runs as a pre-commit hook, scanning for accidental inclusion of production IPs (`172.16.1.`), domains (`chillarin39.com`), and member portal paths.
3. **Network-layer enforcement**: the Kali VM's `iptables OUTPUT` chain DROPs `NEW` connections destined outside the lab CIDR, preventing accidental spillover even if a script ignores the userland guard.
4. **Physical isolation**: `vmbr2` is a slaveless internal bridge with no upstream connectivity, so lab traffic cannot leak to the production VLAN even at L2.

## 6. Account Security Posture

- ChatGPT account is protected by **Passkey / FIDO2 hardware security key** (Advanced Account Security is enabled as of May 2026, ahead of the 2026-06-01 deadline for individual TAC users)
- No password-only authentication
- Session tokens are not shared or stored outside the local browser keychain
- WSL2 SSH keys are separate from any AI integration; AI tools do not have access to production credentials

## 7. Data Handling Discipline

I will not submit the following to any AI model:
- Production credentials (passwords, API keys, SSH private keys)
- Real production IPs / hostnames / service names (substituted with RFC 5737 documentation prefixes `192.0.2.x` / `198.51.100.x` and `example.com` in all published content)
- Customer or personal data (not applicable to my workload)
- Raw production logs (anonymized or replaced with synthetic examples before submission)

A formal individual AI Usage Policy is published at:
https://github.com/chillarin39/openai-tac-application/blob/main/docs/ai-usage-policy.md

## 8. Why a General-Purpose Model Is Insufficient

General-purpose ChatGPT exhibits over-refusal when an article must explain an attack technique side-by-side with its defensive countermeasure (a standard pedagogical pattern for security education). This results in:
- Truncated or evasive explanations that reduce the educational value for Japanese learners who already have limited access to high-quality Japanese-language security material
- Inconsistent depth between the "attack" and "defense" sections of the same article, which contradicts the editorial standard of the guide
- Wasted iteration cycles re-prompting to get past refusals on clearly educational content (e.g., explaining SQL injection mechanics for a chapter on input validation)

TAC's defender-scoped access model fits this exact use case: educational explanation of offensive techniques bounded by a verified defensive context.

## 9. Graduation Plan to GPT-5.5 Cyber (Future)

I am applying for TAC first and intend to graduate to GPT-5.5 Cyber only after demonstrating sustained safe usage. Anticipated milestones:

- **Months 1-3 (TAC, Phase 1-2)**: article authoring and PR review only; no AI-controlled execution
- **Months 4-6 (TAC, Phase 2-3)**: limited HTTP probing of `10.20.0.0/16` targets, optionally via MCP-style tool integration with IP guard enforcement
- **Months 7+ (Cyber upgrade candidate)**: at this point I plan to start the "Graduation Lab" (Chapter 12 of the guide, an end-to-end ACME-corp simulated intrusion exercise) and a separate `redteam-lab` Phase 4 cyber-range mode (note: redteam-lab itself remains out of TAC scope; any AI-assisted activity there will be governed under a separate authorization), both of which would benefit from Cyber-tier capability with documented usage logs from the prior TAC period

## 10. Contact

- Public profile: https://chillablog.chillarin39.com/about/
- GitHub: https://github.com/chillarin39
- Personal Hub: https://chillarin39.com/
- Email: `<insert at submission>`
- Identity verification document: `<provide at submission>` (Japanese government-issued photo ID)

---

## Submission Notes (Internal)

- Replace `<insert at submission>` placeholders with actual values
- Confirm Passkey/FIDO2 is enrolled (DONE 2026-05 — Advanced Account Security active)
- Confirm `ai-usage-policy.md` is publicly accessible at the GitHub URL above
- Confirm `ip_guard.sh` and `ethics_lint.sh` are in place (currently in the private lab repository; canonical path will be referenced once the lab repo is published or extracted into this repository)
- Confirm Phase 0 lab setup (VMID 701-705) is complete and the iptables OUTPUT DROP + production-segment unreachability are verified
- Initial submission targets TAC only; do not request Cyber on first round
- Save submitted final version to `docs/submitted/YYYY-MM-DD-tac-submission.md` (gitignored)
