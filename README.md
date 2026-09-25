# ServiceNow ITSM

## The Business Problem This Lab Solves

When users report IT problems, those problems need to be tracked, routed, prioritised, assigned, worked, and resolved — consistently and auditably. Without a structured system, things fall through the cracks. A server goes down, three people report it to three different team members, nobody knows which one is working on it, and it takes four hours to fix something that should have taken one.

ServiceNow is how most enterprise IT organisations solve this. It is an IT Service Management platform — a structured system for handling every type of IT request, from a password reset to a major infrastructure outage. It enforces process: incidents follow an incident workflow, change requests require approval, service requests come from a catalogue with predefined fulfilment steps.

ServiceNow is one of the most widely deployed enterprise software platforms in the world. If you are going into IT support, you will use it or something that works exactly like it from your first week on the job. Having hands-on experience with it before you start is a meaningful differentiator.

| Role | How this lab applies |
|---|---|
| IT Support / Help Desk | Creating and resolving incidents is the core daily task of every help desk role |
| Sysadmin | Change management — logging, approving, and documenting infrastructure changes |
| IT Service Manager | Building service catalogues, defining workflows, reporting on SLA compliance |
| Cloud Engineer | Cloud operations teams use ServiceNow for change requests, incident management, and service requests for cloud resources |

---

# What You Will Learn

| Skill | Real-world application |
|---|---|
| Create and resolve an Incident | The most common task in every IT support role — done from day one |
| Set ticket priority and SLA | Priority determines response time. SLAs define the commitment to the business. You need to understand both to work in a professional IT environment |
| Assign tickets to queues and individuals | Routing is critical in a team environment — the wrong person working a ticket wastes time and delays resolution |
| Build a service catalogue item | Service catalogues let users self-serve common requests without calling the help desk for every ticket |
| Create a workflow for approvals | Change requests and access requests require manager approval before fulfilment — workflows automate this |
| Run reports on ticket volume and resolution time | Metrics drive IT operations decisions |
| Understand ITIL incident vs problem vs change | The three core ITIL process types |

---

# Step 1 — Get Your Free Instance

1. Go to `developer.servicenow.com`
2. Click **Sign Up** and create a free account — email and password only, no credit card
3. Once logged in, click **Request Instance**
4. Select the latest stable release
5. Click **Request**
6. You will receive an instance URL and login credentials

> **Keep your instance active.** ServiceNow hibernates Personal Developer Instances that haven't been accessed in 10 days and reclaims instances inactive for more than 30 days. Log in at least once a week to keep it active. If it gets reclaimed, you can request a new one for free — but you lose your work.

---

# Step 2 — Navigate the Platform

When you first log in, you are in the ServiceNow admin interface. The left navigation panel gives you access to all modules.

| Module | Where it is | What it does |
|---|---|---|
| Incident | Service Desk → Incidents | The primary module for IT support tickets |
| Problem | Service Desk → Problems | Root cause analysis for recurring incidents |
| Change | Change → Changes | Planned modifications to IT infrastructure |
| Service Catalog | Service Catalog → Catalogs | The user-facing request portal |
| Reports | Reports → Create New | Analytics and metrics |
| Workflow Editor | Process Automation → Flow Designer | Visual workflow builder |

---

# Step 3 — Create and Work an Incident

## Create the Incident

Navigate to:

    Service Desk → Incidents → New

Fill in the incident with the following scenario:

| Field | Value |
|---|---|
| Caller | Abel Tuter |
| Category | Software |
| Subcategory | Email |
| Short description | User cannot access Outlook — error: Cannot connect to server |
| Description | User reports that Outlook stopped working this morning at approximately 9am. Error message: "Cannot connect to the Exchange server. Verify your network settings." Other users in the same building are not affected. User is on a laptop, connected via Wi-Fi. |
| Priority | 3 — Moderate |
| Assignment Group | Service Desk |

Click **Submit**.

Note the incident ticket number.

Example:

    INC0001234

The incident number serves as the unique tracking ID.

---

## Work the Incident

Open the incident that was created.

Change the State to:

    In Progress

Assign the incident to yourself.

Add the following Work Note:

    Contacted user. Confirmed error message. Outlook profile appears corrupted.
    Attempting profile repair. Instructed user to use OWA (webmail) in the interim.
    Resolution ETA: 30 minutes.

Add the following resolution in the **Resolution Notes** field:

    Resolution: Rebuilt Outlook profile. Removed and re-added the Exchange account.
    User confirmed Outlook is working. Issue was a corrupted OST file.
    Closed with user confirmation.

Change the incident State to:

    Resolved → Closed

---

# Step 4 — Build a Service Catalogue Item

Service catalogue items let users request common IT services through a self-service portal without calling the help desk. This reduces ticket volume for routine requests and speeds up fulfilment.

## Create a New Laptop Request Item

Navigate to:

    Service Catalog → Catalogs → Service Catalog

Select:

    Maintain Items → New

Configure the catalogue item:

| Field | Value |
|---|---|
| Name | New Laptop Request |
| Category | Hardware |
| Short description | Request a new or replacement laptop |
| Description | Use this form to request a new laptop for a new hire or to replace a failed or end-of-life device. Requests are reviewed within 2 business days. Delivery takes 5–7 business days after approval. |
| Fulfillment group | IT Hardware Team |
| Price | Leave blank |

Click **Submit** to save the catalogue item.

Open the **Variables** tab and add:

| Variable Name | Type | Mandatory |
|---|---|---|
| Requester Name | Single Line Text | Yes |
| Business Justification | Multi Line Text | Yes |
| Required By Date | Date | Yes |
| Laptop Model Preference | Select Box — Standard, Developer, Executive | No |

Save and preview the item.

The **New Laptop Request** now appears in the service catalogue portal.

---

# Step 5 — Create an Approval Workflow

Change requests require manager approval before work begins. This is a core ITIL control — changes to production infrastructure need authorisation to prevent uncoordinated modifications that could cause outages.

Navigate to:

    Change → Changes → New (Standard)

Create the following sample change request:

| Field | Value |
|---|---|
| Short description | Deploy security patch MS24-001 to all Windows workstations |
| Category | Software |
| Risk | Low |
| Impact | 2 — Medium |
| Start date | Next Saturday at 2:00 AM |
| End date | Next Saturday at 6:00 AM |
| Description | Monthly security patch deployment. Patch addresses CVE-2024-0001 rated CVSS 7.8. Workstations will require one reboot. Deployed via WSUS. Rollback plan: uninstall via WSUS if issues reported post-deployment. |

Under the **Planning** tab, add a:

    Test Plan

and:

    Backout Plan

Click:

    Request Approval

The change moves to:

    Pending Approval

Navigate back to the change and locate the **Approvals** tab.

Approve the change as the admin user.

The change then moves to:

    Scheduled

---

# Step 6 — Build a Report

Navigate to:

    Reports → Create New

Configure the report:

| Field | Value |
|---|---|
| Name | Incident Volume by Priority — Last 30 Days |
| Data | Incident [incident] |
| Type | Bar Chart |
| Group by | Priority |
| Condition | Created is on or after 30 days ago |

Click:

    Save and Run

Build two additional reports:

- **Mean Time to Resolution (MTTR)** — bar chart grouped by Assignment Group
- **Open Incidents by Assigned Agent** — useful for workload balancing

---

# ITIL Concepts to Know

| ITIL Term | Definition | ServiceNow Module |
|---|---|---|
| Incident | An unplanned interruption to a service. Goal: restore service as quickly as possible. | Service Desk → Incidents |
| Problem | The root cause of one or more incidents. Goal: eliminate the root cause permanently. | Service Desk → Problems |
| Change | A planned modification to infrastructure or applications. Goal: implement with minimal risk. | Change → Changes |
| Service Request | A user request for something new such as access, hardware, or information. Not a break/fix. | Service Catalog |
| SLA | Service Level Agreement — the committed response and resolution time for each priority level. | SLA → SLA Definitions |
| CMDB | Configuration Management Database — the record of every IT asset and its relationships. | Configuration → CIs |
| Knowledge Base | Articles documenting known issues and their solutions — reduces repeat incident volume. | Knowledge → Articles |

---

# Portfolio Evidence

Take screenshots of:

- A completed incident with work notes and resolution
- The service catalogue item
- The approval workflow on the change request
- One dashboard report

Write a paragraph for each explaining what process it supports and why it matters in an IT environment.
