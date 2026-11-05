# Lab 2: Social Engineering Toolkit (SET) and Reconnaissance

> **Level:** Intermediate · **Duration:** 2–3 hours  
> **Environment:** Windows 11 host + VMware Workstation + Kali Linux VM (NAT)  
> **Author / Lab report:** Dawit Nigus

## Overview

This lab explores social-engineering concepts, phishing awareness, and OSINT reconnaissance in a controlled environment. It documents the use of SET, Zphisher, GoPhish, Maltego, and Sherlock, then evaluates indicators of compromise, defensive controls, ethics, and cleanup.

**Important:** This is a defensive/educational lab. Use fictional identities and test accounts only. Keep all exercises inside your own VM or an explicitly authorized environment. Never collect real credentials or target real users.

## Objectives

- Understand social-engineering attack vectors and common psychological triggers.
- Recognize how phishing pages and credential-harvesting flows work.
- Compare SET, Zphisher, and GoPhish.
- Use Maltego for visual relationship mapping and Sherlock for username enumeration in fictional scenarios.
- Identify phishing indicators and evaluate defensive countermeasures.
- Practice authorization, responsible reporting, and lab cleanup.

## Lab Environment

| Component | Configuration |
|---|---|
| Host | Windows 11 (25H2) |
| Hypervisor | VMware Workstation |
| VM | Kali Linux (latest) |
| Network | NAT |
| Kali resources | 4 CPU cores, 4 GB RAM, 50 GB virtual disk |
| Desktop | Xfce |
| Tools | SET, Zphisher, GoPhish, Maltego CE, Sherlock |

## Official Downloads & Project Links

- **Kali Linux:** https://www.kali.org/get-kali/
- **VMware Workstation Pro:** https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Pro
- **Social Engineering Toolkit (SET):** https://github.com/trustedsec/social-engineer-toolkit
- **Zphisher (project repository):** https://github.com/htr-tech/zphisher
- **GoPhish:** https://github.com/gophish/gophish
- **Maltego:** https://www.maltego.com/downloads/
- **Sherlock:** https://github.com/sherlock-project/sherlock

> Repository and download pages can change. Follow each project's official installation instructions and review its current status before installing.

## Setup Notes

The report describes installing Kali from the official ISO, selecting Debian 64-bit, allocating 4 cores / 4 GB RAM / 50 GB disk, using NAT, guided LVM partitioning, and the Xfce desktop. It also records verifying network connectivity and checking that the tools are installed.

For a safe practice setup:
- Use a fictional organization (the lab uses **FinanceCorp**) and fictional test users.
- Use localhost or a private VM address only.
- Do not expose phishing infrastructure through public tunnels.
- Do not use real company login pages or real user credentials.

## Exercise 1 — SET (Social Engineering Toolkit)

**Goal in the source lab:** Understand the credential-harvester workflow and examine the visual and technical indicators of a fake login page.

### Learning observations

- SET's site-cloning workflow automates much of the page-copying process.
- A raw IP address, a mismatched domain, missing HTTPS, browser warnings, or incomplete page behavior can expose a fake page.
- HTTPS/padlock alone is not proof that a site is legitimate; users must verify the domain.
- Defenders should monitor unusual login pages, domains, and form submissions.

### Defensive indicators

- URL does not match the legitimate organization's domain.
- Browser shows “Not Secure” or certificate/domain warnings.
- Page behavior differs from the legitimate login flow.
- A password manager refuses to autofill on an unfamiliar domain.
- An unexpected HTTP POST sends form data to an unfamiliar host.

## Exercise 2 — Zphisher

The lab compares Zphisher's prebuilt templates with SET's on-demand site cloning. It discusses why convincing branding can fool users and how defenders can identify suspicious infrastructure.

### Defensive controls

- DNS/domain reputation filtering and newly registered-domain monitoring.
- Browser phishing protection and email link analysis.
- User awareness focused on verifying the full domain.
- Password managers and MFA.
- Block or investigate suspicious tunnel domains and redirects.

## Exercise 3 — GoPhish Campaign Management

GoPhish is documented as a campaign-oriented platform for authorized simulations. The lab describes sending profiles, test-user groups, campaign setup, and exported results.

### Useful simulation metrics

| Metric | What it measures |
|---|---|
| Open rate | Subject/sender engagement |
| Click rate | Link/pretext interaction |
| Submission rate | Risky form interaction in a controlled simulation |
| Report rate | Users who report suspicious messages |
| Time to report | Speed of defensive response |

Use simulations for learning and improvement—not punishment. Keep individual results confidential and provide supportive follow-up training.

## Exercise 4 — Maltego OSINT

The lab uses a graph to map a **fictional** organization's domain and relationships. Relationship mapping can help analysts understand how domains, DNS, email addresses, and public references connect.

### Sources described

- WHOIS / registrar records
- DNS records (subdomains, mail servers, name servers, IPs)
- Search engines and public web content
- Social profiles and public mentions
- Historical website snapshots

**Defensive use:** Audit your organization's public footprint and remove or limit unnecessary exposure. Do not use personal information to target real people.

## Exercise 5 — Sherlock Username Enumeration

The lab checks username reuse across platforms using fictional usernames. Reuse can link otherwise separate accounts and reveal profile details, interests, affiliations, or location clues.

### Privacy recommendations

- Use distinct usernames across unrelated services.
- Restrict profile visibility and remove unnecessary public personal details.
- Review public profile photos, bios, and location data.
- Periodically audit your own digital footprint.
- Avoid exposing account-recovery hints.

## Exercise 6 — Integrated Scenario: FinanceCorp

The source lab combines reconnaissance, fictional employee profiles, pretext analysis, a controlled simulation, and reporting. Keep the scenario strictly fictional and use only authorized test accounts.

### Defensive lessons

- Authority and urgency are common manipulation triggers.
- Verify sensitive requests through a separate trusted channel.
- Use MFA and least privilege to reduce account-compromise impact.
- Provide a clear, blame-free phishing-reporting channel.
- Reduce unnecessary employee and infrastructure information exposure.

## Phishing Indicators of Compromise (IOCs)

- DNS or web requests to newly registered, unfamiliar, or look-alike domains.
- Suspicious redirects or multiple URL hops.
- Login-style pages on unexpected domains.
- POST requests to unfamiliar external hosts after a link click.
- Email authentication failures or suspicious sender/display-name mismatch.
- Authentication from unusual IPs or locations after a suspected credential exposure.
- Password-manager autofill mismatch or browser phishing warnings.

## Defensive Best Practices

### For individuals
- Verify the complete domain before signing in.
- Treat urgency and unexpected authority requests with caution.
- Use a password manager and MFA.
- Confirm sensitive requests through a separate channel.
- Limit personal information shared publicly.

### For organizations
- Enforce SPF, DKIM, and DMARC.
- Use email filtering, link sandboxing, DNS filtering, and endpoint monitoring.
- Require MFA and least-privilege access.
- Run authorized, non-punitive awareness simulations.
- Establish a simple “Report Phishing” process.
- Monitor brand impersonation and reduce public OSINT exposure.
- Segment networks and prepare an incident-response process.

## Incident Response Checklist

1. Disable or secure the affected account/device as appropriate.
2. Reset credentials and re-register MFA if compromise is suspected.
3. Revoke active sessions and tokens.
4. Preserve the suspicious email, headers, URLs, and relevant logs.
5. Identify other recipients and determine whether credentials or malware were involved.
6. Review authentication logs for unusual activity.
7. Block malicious domains/URLs and notify the appropriate security team.
8. Provide supportive follow-up training and document lessons learned.

## Ethical Boundaries & Rules of Engagement

- Obtain written authorization from the system or business owner.
- Define scope, target accounts, dates, permitted techniques, and stop conditions.
- Use fictional names, domains, and test accounts.
- Do not send phishing messages to real people without an approved engagement.
- Do not access real social accounts or collect real credentials.
- Keep testing inside the VM/private lab; do not publish captured data.
- Report findings privately and responsibly.
- Treat simulation failures as training opportunities, not grounds for public shaming.

## Cleanup

The report documents stopping lab services and removing test data after exercises. Confirm that:
- GoPhish is stopped.
- Apache/SET listener is stopped.
- Zphisher processes are stopped.
- Test capture files and reports are deleted.
- GoPhish test database is reset or safely archived as needed.
- Any temporary lab infrastructure is removed.

## Key Takeaways

- SET, Zphisher, and GoPhish have different roles: framework, template-oriented demonstration tool, and campaign-management platform.
- Maltego and Sherlock show how public information can be correlated into a detailed profile.
- HTTPS encrypts a connection but does not establish that a domain is legitimate.
- Strong MFA, domain verification, email authentication, reporting channels, and awareness training reduce phishing risk.
- Authorization, scope, privacy, and responsible reporting are essential to ethical security testing.

## References

- SET: https://github.com/trustedsec/social-engineer-toolkit
- Zphisher: https://github.com/htr-tech/zphisher
- GoPhish: https://github.com/gophish/gophish
- Maltego: https://www.maltego.com/
- Sherlock: https://github.com/sherlock-project/sherlock
- Kali Linux: https://www.kali.org/get-kali/
- VMware Workstation: https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Pro
