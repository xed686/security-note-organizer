# Case Anchor Library

Used in Step 5: attach a real business case to each key knowledge point. Look it up by vulnerability / technique type.

## Usage rules

1. Tell every case in four beats: **what happened -> root cause matching which link in the notes -> business consequence
   -> takeaway for a pentester**.
2. The tables below give only the **skeleton of the incident**. Before writing details (year, scale, amounts) into the
   notes, verify them if you have web access, using **only non-mainland-China sources** (NVD, vendor security advisories,
   regulator announcements, authoritative English-language media). If you cannot verify, describe only the nature of the
   incident, with no specific numbers.
3. When no suitable case exists, substitute an "example scenario" and label it clearly. Never write fictional content as a
   real incident.
4. Cases exist to show **why this knowledge point is worth learning**, not to serve as an attack tutorial.

## Contents
- Web application
- Components and supply chain
- Permissions and authentication
- System and internal network
- Generic: how to write an example scenario when no case exists
- Generic: how to swap cases for non-vulnerability knowledge (tooling, architecture, methodology)

---

## Web application

| Type | Case | Root cause (matching knowledge point) | Business takeaway |
| --- | --- | --- | --- |
| SQL Injection | Heartland Payment Systems breach (disclosed around 2008–2009), entry vector reported as SQL Injection, ultimately leading to large-scale theft of payment card data | User input concatenated into queries; after the external entry point was breached, the attacker moved deeper | One injection point can be the way into the internal network, not just "reading a few rows" |
| SQL Injection | TalkTalk 2015 breach, involving SQL Injection, later fined by the UK regulator | Legacy pages / legacy systems lacking input handling | Legacy systems and edge businesses are vulnerability hot spots — cover them during reconnaissance |
| Stored XSS | Samy worm (MySpace, 2005), spreading rapidly via stored XSS | User content output to other users without escaping; script executes under the victim's identity | The power of XSS is "acting as the victim" — it can spread worm-style |
| SSRF | Capital One 2019 incident, using server-side request forgery to reach the cloud metadata service and obtain credentials | The server issues requests on the user's behalf and can reach internal / metadata addresses | SSRF does far more damage in cloud environments — always think of the metadata service |
| Unauthorized access / IDOR | Optus 2022 incident, publicly reported as an API lacking access control with enumerable identifiers, exposing large amounts of user information | The endpoint does not check "may this person access this record" | When testing endpoints, change the ID, change the identity, drop authentication — verify access control on every resource |
| File inclusion (LFI -> RCE) | CVE-2018-12613 in phpMyAdmin (4.8.0 / 4.8.1): the `target` parameter of `index.php` is concatenated into an include path and, via double decoding and filter chains, ends in RCE | User input reaches the include path directly, with no allow-list mapping | The end of LFI is often RCE, not "file read" — rate the report by the real impact; allow-list mapping is the fix |
| Path traversal / arbitrary file read | CVE-2021-41773 and CVE-2021-42013 (Apache HTTP Server 2.4.49 / 2.4.50): encoded `../` bypasses normalization, allowing arbitrary file reads and, with `mod_cgi` enabled, RCE | Broken path normalization; upgrades skipped the incomplete patched version | Middleware version is a must-check in reconnaissance; an old version is an entry point by itself |
| File upload | CVE-2017-12615 (Apache Tomcat allows `PUT` to write arbitrary files, e.g. a JSP backdoor) | Dangerous HTTP methods not disabled + executable upload directory | "Upload point" is not only form uploads — think `PUT`/`PATCH` too; a non-executable upload directory is a hard line of defense |

## Components and supply chain

| Type | Case | Root cause | Business takeaway |
| --- | --- | --- | --- |
| Known-vulnerable component left unpatched | Equifax 2017 incident, involving an Apache Struts vulnerability (CVE-2017-5638), left unpatched after a fix was released | Incomplete asset inventory, failed patch management | Identifying frameworks and versions during reconnaissance is one of the highest-leverage pentest steps |
| RCE in a logging component | Log4Shell (CVE-2021-44228), the JNDI lookup issue in Apache Log4j 2 — triggerable simply by logging a user-controlled string | The logging library "parsed" user input when it should not have | "Indirect paths": any input that gets logged or parsed is worth testing |
| Command injection | Shellshock (CVE-2014-6271), a Bash environment-variable handling flaw, triggered remotely via CGI and similar paths | Content in environment variables executed as commands | Old components hide where you least expect — think hard about CGI and embedded devices |
| File processing chain | GitLab CVE-2021-22205, remote code execution triggered by ExifTool parsing an uploaded image | The server-side "second-pass processing" component was vulnerable | File upload risk is not only the extension check, but how the server parses the file |

## Permissions and authentication

| Type | Case | Root cause | Business takeaway |
| --- | --- | --- | --- |
| Credential leak / no MFA | Colonial Pipeline 2021 incident, with public reporting pointing to a VPN account credential without multi-factor authentication | Credential reuse / weakly protected remote entry points | VPN and remote management entry points are high-value targets; credential attacks are cheap with high payoff |
| Weak / default passwords | Large numbers of IoT devices and admin consoles taken over in bulk through default passwords (e.g. the Mirai botnet) | Default configuration never changed | After asset discovery, a default-password check is mandatory |

## System and internal network

| Type | Case | Root cause | Business takeaway |
| --- | --- | --- | --- |
| Linux privilege escalation | Dirty COW (CVE-2016-5195), a Linux kernel race condition allowing local privilege escalation | Race condition in kernel memory management | Once you have a low-privilege shell, kernel version and known privilege-escalation flaws are the first thing to check |
| Windows privilege escalation / lateral movement | PrintNightmare (CVE-2021-34527), a vulnerability related to the Windows Print Spooler | A high-privilege service enabled by default exposes attack surface | In a domain environment, an "inconspicuous default service" can be the way into escalation and lateral movement |
| Internal lateral movement | NotPetya (2017), spreading fast internally by combining exploits such as EternalBlue (MS17-010) with credential theft | No internal segmentation, missing patches, stealable credentials | The core of internal penetration is the combination of "credentials + network reachability + unpatched services" |

---

## When no case exists: how to write an example scenario

Write it like this, and include the words "Example scenario":

> **Example scenario**: an e-commerce "order lookup" endpoint `/api/order?id=1001` concatenates `id` straight into SQL.
> A normal user only passes their own order number, but an attacker changes the parameter to ... (matching step 2 of
> section 1.3 in these notes). The consequence: any user's orders, phone numbers, and addresses can be read — a personal
> information leak, exposing the company to regulator penalties and loss of user trust.

Key points:

1. Choose **business nouns** (orders, coupons, invoices, membership, payment callbacks), not an abstract "some system".
2. State explicitly **which step in the notes it corresponds to**.
3. Make the **business consequence** clear: what leaked, who was affected, what problems the company faces.

---

## Non-vulnerability knowledge: how to swap the case

When the knowledge point is about tooling, architecture, or methodology (e.g. "the workflow form of an agent",
"orchestration layer vs execution layer"), real security incidents usually do not fit. Swap the parts below — **do not
invent a "company X was breached" story to fill the slot**.

| Original part | Replace with | Requirement |
| --- | --- | --- |
| Real vulnerability incident (four beats) | **Product case**: pick 1–2 real open-source projects or products and write four beats: what it is -> what its key design is -> what that design solves -> how a learner should use it | Must be written after checking the project README / official docs; include star count, license, and last commit date when available; if you cannot check, downgrade to "example" |
| Code comparison (source/sink) | **Structure / layering diagram** (mermaid or indented arrows) showing who calls whom and what each layer owns | The diagram must stand on its own without the surrounding prose |
| "Takeaway for a pentester" | **Selection judgment**: which task to use it for, which task not, and the cost of choosing wrong | Give actionable criteria, not "it depends" |

> The rule for example scenarios is unchanged: anything you construct yourself is labeled "Example scenario" and never
> written up as a real project's capability.
