
# Best Practices for Writing Solution Guides <!-- omit in toc -->

A framework for creating enterprise-grade solution guides for Ansible Automation Platform.

- [0. Title Standard (Non-Negotiable)](#0-title-standard-non-negotiable)
- [1. The Executive Hook (Strategic Framing)](#1-the-executive-hook-strategic-framing)
  - [1.1 The Problem Statement (2-4 sentences max)](#11-the-problem-statement-2-4-sentences-max)
  - [1.2 Who Benefits (Persona Mapping)](#12-who-benefits-persona-mapping)
- [2. Scope and Production Considerations (Expectation Setting)](#2-scope-and-production-considerations-expectation-setting)
  - [2.1 Impact Rating](#21-impact-rating)
  - [2.2 Prerequisites](#22-prerequisites)
  - [2.3 Cost and Resource Notes](#23-cost-and-resource-notes)
  - [2.4 KB Article Metadata](#24-kb-article-metadata)
- [3. Architecture and Workflow (The "Aha" Layer)](#3-architecture-and-workflow-the-aha-layer)
  - [3.1 Workflow Diagram](#31-workflow-diagram)
  - [3.2 Narrative Walkthrough](#32-narrative-walkthrough)
  - [3.3 Visual Design Patterns](#33-visual-design-patterns)
- [4. Technical Core (The Executable Proof)](#4-technical-core-the-executable-proof)
  - [4.1 Foundation Setup](#41-foundation-setup)
  - [4.2 Featured Code (Critical Section)](#42-featured-code-critical-section)
  - [4.3 AAP Integration](#43-aap-integration)
- [5. Validation and Sanity Check](#5-validation-and-sanity-check)
  - [5.1 The Test](#51-the-test)
  - [5.2 Expected Result](#52-expected-result)
- [6. Business Reinforcement and Maturity Path](#6-business-reinforcement-and-maturity-path)
  - [6.1 ROI Recap](#61-roi-recap)
  - [6.2 Crawl, Walk, Run](#62-crawl-walk-run)
  - [6.3 Next Steps and Cross-Linking](#63-next-steps-and-cross-linking)
- [Quality Scoring Model (Internal Use)](#quality-scoring-model-internal-use)
- [Common Failure Modes (What to Ban)](#common-failure-modes-what-to-ban)
- [What Makes a Guide "Elite"](#what-makes-a-guide-elite)
- [Final Recommendation](#final-recommendation)
- [Appendix: Starter Template](#appendix-starter-template)

---

## 0. Title Standard (Non-Negotiable)

**Rule:** Titles must describe an operational outcome, not a product feature.

Solution guides published on access.redhat.com follow the convention `[Topic] - Solution Guide`. Within that convention, the topic portion should still be outcome-oriented whenever possible.

**Bad:**

- "Using the ServiceNow Collection"
- "Ansible EDA Overview"

**Good (KB title format):**

- "ServiceNow ITSM Ticket Enrichment Automation - Solution Guide"
- "AIOps automation with Ansible - Solution Guide"

**Better (outcome-oriented):**

- "Reducing MTTR with Automated ServiceNow Ticket Enrichment - Solution Guide"
- "Triggering Automated Remediation from Splunk Alerts with Event-Driven Ansible - Solution Guide"

> When in doubt, use the `[Topic] - Solution Guide` format for the KB article title, but lead the guide itself with an outcome-oriented subtitle or problem statement in the opening section.

**Checklist:**

- [ ] Does the title describe a business or operational outcome?
- [ ] Does the title follow the `[Topic] - Solution Guide` convention for KB publishing?
- [ ] Would a VP of IT understand the value without knowing Ansible?

---

## 1. The Executive Hook (Strategic Framing)

This section must be readable by a decision maker.

### 1.1 The Problem Statement (2-4 sentences max)

- Define the operational pain.
- Quantify if possible (time, cost, risk, compliance).

**Example format:**

> Organizations spend X hours manually performing Y, leading to Z risk. This guide demonstrates how to automate this workflow using AAP to reduce effort by X% and improve consistency.

### 1.2 Who Benefits (Persona Mapping)

| Persona | What They Gain |
|---------|---------------|
| IT Ops Admin | Eliminates manual triage |
| Architect | Reference workflow design |
| Manager | Reduced MTTR and measurable ROI |

**Checklist:**

- [ ] Is the operational pain explicit?
- [ ] Is the value framed in business terms?
- [ ] Is there at least one quantified benefit?

---

## 2. Scope and Production Considerations (Expectation Setting)

This is where many solution guides fail.

### 2.1 Impact Rating

- **Low** — safe, read-only
- **Medium** — config change, reversible
- **High** — production mutation, requires CAB

### 2.2 Prerequisites

- AAP version
- Collections
- OS requirements
- External systems (ServiceNow, Splunk, AWS, etc.)

### 2.3 Cost and Resource Notes

- GPU required?
- Cloud instance sizing?
- API limits?
- Licensing assumptions?

**Checklist:**

- [ ] Are version numbers explicitly listed?
- [ ] Is the required infrastructure realistic?
- [ ] Are security or RBAC implications mentioned?

### 2.4 KB Article Metadata

Published solution guides on access.redhat.com follow a structured metadata pattern. Include these fields near the top of each guide, directly after the overview:

**Operational Impact:** State the impact level per step if it varies, not just per guide.

| Impact | Meaning |
|--------|---------|
| **None** | Read-only, no changes to systems |
| **Low** | Safe, reversible changes |
| **Medium** | Configuration changes, test first |
| **High** | Production mutation, requires change advisory board (CAB) |

**Business Value Drivers:** 2-3 bullet points framing the business outcome (e.g., reduced downtime, improved compliance posture).

**Technical Value Drivers:** 2-3 bullet points framing the technical outcome (e.g., simplified compliance reporting, enforced configuration policies).

**Recommended Demos and Self-Paced Labs:** Link to interactive demos, YouTube videos, and Instruqt labs where available.

**Featured Ansible Content Collections:** List every collection used in the guide with a direct link to its Automation Hub page.

**Checklist:**

- [ ] Is operational impact stated?
- [ ] Are business and technical value drivers listed?
- [ ] Are recommended demos or labs linked?
- [ ] Are featured collections listed with Automation Hub links?

---

## 3. Architecture and Workflow (The "Aha" Layer)

This must show causality.

### 3.1 Workflow Diagram

Simple. Clean. 3-6 blocks max.

```
Event → EDA Rule → Playbook → API Call → Result
```

### 3.2 Narrative Walkthrough

Explain the logic in 5-8 sentences:

- What triggers it
- What decision logic runs
- What automation executes
- What outcome is produced

**Checklist:**

- [ ] Could someone redraw this workflow after reading?
- [ ] Is the automation deterministic and clear?

### 3.3 Visual Design Patterns

Use the right visual format for the right purpose:

| Format | When to Use | Example |
|--------|-------------|---------|
| **Workflow diagram** | Show end-to-end causality (3-6 blocks) | Event -> EDA -> Playbook -> Result |
| **Architecture diagram** | Show system components and connections | AAP <-> Kafka <-> Observability tool |
| **Tables** | Compare options, map events to responses | Event / Source / Response tables |
| **Code blocks (YAML)** | Show the actual automation logic | Featured tasks, rulebooks, API calls |
| **Screenshots** | Show AAP UI configuration (Job Templates, Workflows) | Workflow Visualizer, Survey setup |
| **Callout boxes** | Highlight tips, warnings, and context | Blockquotes with tip/warning prefix |

**Callout conventions:**

Use blockquotes for tips, warnings, and contextual notes. Keep a consistent style across all guides:

> **Tip:** Use for helpful context, shortcuts, or "did you know" information.

> **Why [tool]?** Use for explaining tool choices and alternatives.

> **Warning:** Use for production-impact notes or common mistakes.

**Inline logos and branding:**

When referencing third-party tools (Kafka, Splunk, ServiceNow, etc.), include their logo image inline where it aids scannability. Keep logos to a consistent width (e.g., 200px) and link to the relevant Automation Hub page.

**Checklist:**

- [ ] Is there at least one workflow or architecture diagram?
- [ ] Are tables used for comparisons instead of long prose?
- [ ] Are callout boxes used consistently?

---

## 4. Technical Core (The Executable Proof)

This is where credibility is built.

### 4.1 Foundation Setup

Only include:

- Secrets/tokens
- API connectivity
- Required collections

**Automation Hub linking rule:** Every Ansible collection referenced in the guide **must** include a direct link to its page on [Automation Hub](https://console.redhat.com/ansible/automation-hub/). This serves as both a credibility signal and a convenience for the reader.

**Example:**

- **Certified Collection**: [redhat.ai](https://console.redhat.com/ansible/automation-hub/repo/published/redhat/ai) -- Configures and serves an AI model using InstructLab.
- **Validated Collection**: [infra.ai](https://console.redhat.com/ansible/automation-hub/repo/validated/infra/ai) -- Provisions RHEL AI infrastructure.

No fluff.

### 4.2 Featured Code (Critical Section)

Do **NOT** dump the full repo. Show:

- The key task
- The logic block
- The rulebook trigger
- The API call

**Example:**

```yaml
- name: Update ServiceNow ticket with enriched data
  servicenow.itsm.incident:
    number: "{{ incident_number }}"
    state: "In Progress"
    work_notes: "{{ ai_summary }}"
```

Then link to the full source:

> Full source available at: `github.com/your-org/solution-guide-x`

**Checklist:**

- [ ] Is there copy-pasteable code?
- [ ] Is the critical automation logic visible?
- [ ] Is there a GitHub repo link?

### 4.3 AAP Integration

Show:

- Job Template setup
- Rulebook activation
- Credentials mapping
- RBAC notes

No vague instructions like "Create a job template." Be explicit.

---

## 5. Validation and Sanity Check

This is mandatory.

### 5.1 The Test

- Trigger a webhook
- Run a test job
- Submit a dummy ticket

### 5.2 Expected Result

Show:

- Console output snippet
- UI success indicator
- Ticket state change

**Checklist:**

- [ ] Is there a clear test?
- [ ] Is there a clear expected output?
- [ ] Can failure be diagnosed?

---

## 6. Business Reinforcement and Maturity Path

This prevents it from being "just a lab."

### 6.1 ROI Recap

> You now have automated X, reducing manual effort and improving consistency.

### 6.2 Crawl, Walk, Run

| Maturity | Description |
|----------|-------------|
| **Crawl** | Read-only enrichment |
| **Walk** | Automated ticket updates |
| **Run** | Fully automated remediation |

### 6.3 Next Steps and Cross-Linking

Every guide exists within a broader ecosystem. Authors must identify and link to related guides so readers understand the full journey.

- Link to the **next logical guide** (e.g., Network Fact Gathering links to Network Backup and Configuration)
- Link to **prerequisite guides** (e.g., AIOps guide references the AI Infrastructure guide for deploying the AI backend)
- Link to **ISV or partner integrations** where applicable
- Link to **advanced architecture expansions** for readers ready to go deeper

**Example cross-links:**

> **Related guides:**
> - Need to deploy the AI infrastructure first? See [AI Infrastructure automation with Ansible](README-IA.md)
> - Ready to add event-driven triggers? See [Get started with EDA](https://access.redhat.com/articles/7136720)

**Checklist:**

- [ ] Does the guide fit into a broader journey?
- [ ] Is there a next logical step?
- [ ] Are prerequisite guides linked?
- [ ] Are complementary guides cross-referenced?

---

## Quality Scoring Model (Internal Use)

You can now grade guides objectively:

| Category | Weight |
|----------|--------|
| Outcome Clarity | 20% |
| Architecture Clarity | 20% |
| Technical Executability | 25% |
| Validation/Testability | 15% |
| Production Readiness Info | 10% |
| Business Framing | 10% |

Score each 1-5. Anything below 3 in any category — revise before publish.

---

## Common Failure Modes (What to Ban)

- "Overview Only" guides with no code
- Screenshot-heavy, YAML-light content
- No validation step
- No versioning
- No production impact warning
- No persona/value framing
- No GitHub repo

---

## What Makes a Guide "Elite"

A truly excellent solution guide:

- Has a deterministic workflow
- Shows real automation logic
- Can be executed in < 60 minutes
- Has clear operational outcome
- Maps to maturity progression
- Could be used by a field seller as enablement

---

## Final Recommendation

You should:

1. **Turn this into a formal publishing rubric.**
2. **Require authors to submit the checklist with each guide.**
3. **Reject guides that don't include:**
   - Featured code
   - Validation step
   - Outcome-oriented title
   - Architecture diagram

---

## Appendix: Starter Template

Copy this skeleton when creating a new solution guide. Replace all placeholder text.

````markdown
# [Topic] - Solution Guide

> **Knowledge Base Article**: [https://access.redhat.com/articles/XXXXXXX](https://access.redhat.com/articles/XXXXXXX)

## Overview

<!-- 2-4 sentence problem statement. Define the operational pain and quantify if possible. -->

Organizations spend X hours manually performing Y, leading to Z risk. This guide demonstrates how to automate this workflow using Ansible Automation Platform.

**Operational Impact:** Low | Medium | High

**Business Value Drivers:**
- [Value 1]
- [Value 2]

**Technical Value Drivers:**
- [Value 1]
- [Value 2]

**Recommended Demos and Self-Paced Labs:**
- [Demo or lab name](https://link)

**Featured Ansible Content Collections:**
- [collection.name](https://console.redhat.com/ansible/automation-hub/repo/published/namespace/name/)

### Who Benefits

| Persona | What They Gain |
|---------|---------------|
| IT Ops Admin | [Benefit] |
| Architect | [Benefit] |
| Manager | [Benefit] |

## Prerequisites

- Ansible Automation Platform version X.X
- Collections: `namespace.collection` vX.X
- OS: RHEL X
- External systems: [ServiceNow, AWS, etc.]

## Architecture

<!-- Include a workflow diagram: 3-6 blocks showing the end-to-end flow. -->

```
[Trigger] → [Step 1] → [Step 2] → [Result]
```

<!-- 5-8 sentence narrative explaining what triggers the workflow, what logic runs, and what outcome is produced. -->

## Solution Walkthrough

### Step 1: [Name]

**Operational Impact:** Low

<!-- Explanation of what this step does. -->

```yaml
- name: Example task
  namespace.collection.module:
    parameter: "{{ variable }}"
```

### Step 2: [Name]

**Operational Impact:** Medium

<!-- Continue with additional steps. -->

## Validation

### Test

<!-- Describe how to trigger and test the automation. -->

### Expected Result

<!-- Show expected console output, UI indicator, or state change. -->

```
[Expected output here]
```

## Business Reinforcement

### ROI Recap

> You now have automated [X], reducing manual effort by [Y] and improving [Z].

### Maturity Path

| Maturity | Description |
|----------|-------------|
| **Crawl** | [Starting point] |
| **Walk** | [Intermediate] |
| **Run** | [Fully automated] |

### Related Guides

- [Related guide 1](link)
- [Related guide 2](link)

## Sources

- [Red Hat Ansible Automation Platform](https://www.redhat.com/en/technologies/management/ansible)
- [Additional source](link)
````
