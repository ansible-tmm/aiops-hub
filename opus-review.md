
# Review: Solution Guides and Knowledge Base Articles

*Reviewed: February 16, 2026*

---

## Part 1: Best Practices Document Review

The best practices framework is strong — it provides a clear, opinionated structure that would meaningfully raise the quality bar for future guides. Below are suggestions for improvement, grounded in what I observed reviewing the two existing guides (README-AIOps.md and README-IA.md) and all eight KB articles.

### What Works Well

- **Checklist-driven approach**: The per-section checklists make this actionable for authors and reviewable for editors.
- **Quality Scoring Model**: Having a weighted rubric brings objectivity to what is typically a subjective review process.
- **Common Failure Modes**: Calling out anti-patterns explicitly is valuable — especially "Overview Only guides with no code" and "Screenshot-heavy, YAML-light content."
- **Crawl/Walk/Run maturity model**: This is a great concept. Neither existing guide implements it yet, which shows there is room to lead by example.

### Suggestions for Improvement

#### 1. Add a Starter Template / Skeleton

The framework describes *what* each section should contain but does not provide a copy-paste skeleton. Authors would benefit from a markdown template file they can duplicate and fill in. This would dramatically reduce friction and increase consistency across guides.

#### 2. Acknowledge the KB Article Metadata Pattern

Several published KB articles on access.redhat.com include structured metadata fields that the best practices document does not mention:

- **Operational Impact** (None / Low / Medium / High) — per section, not just per guide
- **Business Value Drivers** and **Technical Value Drivers** — as bullet points
- **Recommended Demos and Self-Paced Labs** — links to interactive labs and videos
- **Featured Ansible Content Collections** — explicit collection links to Automation Hub

The best practices doc should incorporate these as a required section, since this is the pattern already established on the published platform.

#### 3. Add Guidance on Linking to Automation Hub Collections

Both existing guides do this well — linking to `console.redhat.com/ansible/automation-hub/...` for every collection mentioned. This should be an explicit best practice rule: *"Every Ansible collection referenced must include a direct link to its Automation Hub page."*

#### 4. Add a Section on Visual Design Patterns

The existing guides use several visual techniques that are effective but not documented:

- Emoji-styled callout boxes (tip, question, warning patterns)
- Inline logos for third-party tools (Kafka, Splunk, Instana, etc.)
- Tables for event/source/response mappings (AIOps guide does this very well)
- Clickable workflow diagrams

The best practices doc should specify when to use diagrams vs. screenshots vs. tables vs. code blocks.

#### 5. Address Cross-Linking Between Guides

The network guides (Fact Gathering and Backup/Config) link to each other with a "Next Steps" reference. The AIOps and IA guides do not cross-reference at all, despite being complementary (IA deploys the AI infrastructure that AIOps consumes). Best practices should require authors to identify and link related guides.

#### 6. Reconcile the Title Standard with Reality

The title standard says titles must describe an operational outcome ("Reducing MTTR with..."). However, every published KB article uses a simpler pattern: `[Topic] - Solution Guide`. This is not necessarily wrong — it is consistent and scannable. The best practices should either:
- Update the rule to match the established convention, or
- Provide both a "KB title" (for access.redhat.com) and a "subtitle" (outcome-oriented) pattern

#### 7. Add Version Tracking Guidance

None of the existing guides include a "last updated" date, AAP version tested, or changelog. For production guides that reference specific API endpoints, collection versions, and cloud services, this is a real gap. Best practices should require at minimum:
- Date last reviewed
- AAP version(s) tested against
- Collection versions used

#### 8. Expand the Validation Section with AAP-Specific Patterns

Section 5 lists generic validation ideas (trigger a webhook, run a test job). It should include AAP-specific validation patterns:
- How to verify a Job Template runs successfully (check job output in Controller)
- How to validate an EDA rulebook activation is listening
- How to confirm a workflow template chain completes end-to-end
- Example `curl` commands for API validation (the IA guide does this well)

#### 9. Self-Grade the Existing Guides

The best practices document would carry more weight if it included a self-assessment of the two existing guides against its own rubric. This demonstrates transparency and gives authors a concrete reference for "here is what an 8/10 looks like vs. a 6/10."

---

## Part 2: Knowledge Base Article Reviews

Each article is graded on a 1-10 scale using the quality scoring categories from the best practices framework: Outcome Clarity, Architecture Clarity, Technical Executability, Validation/Testability, Production Readiness Info, and Business Framing.

---

### 1. Automation Dashboard and Analytics - Solution Guide

**Link**: https://access.redhat.com/articles/7136383
**Grade: 8 / 10**

**Strengths:**
- Excellent persona mapping (Technical Teams, Operational Managers, Leadership) with specific value propositions for each
- Thorough step-by-step setup instructions for the Automation Dashboard (5-step walkthrough)
- Good metrics tables explaining what each dashboard component measures
- Includes both on-premise (Dashboard) and cloud-based (Analytics) paths
- Strong "Next Steps" section with actionable follow-ups

**Weaknesses:**
- No architecture or workflow diagram showing how Dashboard connects to AAP instances
- Very long and dense — could benefit from a visual overview at the top
- The Automation Calculator section reads like product documentation rather than a solution guide
- No explicit problem statement with quantified pain (e.g., "teams spend X hours compiling ROI reports manually")
- No featured code / playbook examples — this is the only guide with zero YAML

**Suggestions:**
- Add a simple architecture diagram: AAP Instance -> OAuth2 -> Dashboard -> Reports
- Add a 2-3 sentence problem statement at the top quantifying the pain
- Consider splitting into two guides (Dashboard + Analytics) given the length
- Include a sample `clusters.yaml` configuration as featured code

---

### 2. Get started with EDA (Ansible Rulebook) - Solution Guide

**Link**: https://access.redhat.com/articles/7136720
**Grade: 8 / 10**

**Strengths:**
- Excellent hands-on approach with clear test scenarios (matching vs. non-matching messages)
- Shows both webhook and Kafka sources — covering dev and production patterns
- Includes actual terminal output showing what success and failure look like
- Good explanation of core components (Action, Condition, Source)
- Demonstrates dynamic event data passthrough (sender example)

**Weaknesses:**
- Title is procedural ("Get started with...") rather than outcome-oriented
- No architecture diagram showing the event flow
- No explicit business framing / problem statement
- Missing a validation section separate from the tutorial steps
- The Kafka example assumes infrastructure is already running — no setup guidance for the Kafka broker
- No crawl/walk/run maturity path

**Suggestions:**
- Add a simple flow diagram: Event Source -> Rulebook Engine -> Condition Match -> Action
- Add a brief problem statement: "Manual alert triage costs teams X hours/week..."
- Include a note on how to test in AAP (not just CLI `ansible-rulebook`)
- Add maturity progression: Webhook dev testing -> Kafka production -> Event Streams multi-source

---

### 3. AI Infrastructure automation with Ansible - Solution Guide

**Link**: https://access.redhat.com/articles/7118390
**Grade: 7 / 10**

**Strengths:**
- Clear, well-structured walkthrough from provisioning to validation
- Good collection references (infra.ai and redhat.ai) with Automation Hub links
- Provides both CLI and AAP workflow paths
- Includes validation via both curl and the redhat.ai.completion module
- Good "Final Notes" section on extensibility

**Weaknesses:**
- No executive hook / problem statement (jumps straight to "Background")
- No persona mapping — who is this for?
- Workflow template screenshot is mentioned but relies on external hosting
- No operational impact rating
- No business value framing or ROI discussion
- No maturity path (e.g., single model -> multi-model -> fine-tuned)
- Collection version numbers and AAP version not specified

**Suggestions:**
- Add a 2-sentence problem statement: "Provisioning AI infrastructure manually is error-prone and time-consuming..."
- Add operational impact and business/technical value driver sections (like the network guides have)
- Specify tested AAP version and collection versions
- Add a crawl/walk/run: Provision on CLI -> Automate via AAP workflow -> Integrate with Lightspeed

---

### 4. AIOps automation with Ansible - Solution Guide

**Link**: https://access.redhat.com/articles/7119667
**Grade: 7 / 10**

**Strengths:**
- Comprehensive and ambitious — covers the full AIOps lifecycle in a single guide
- Excellent reference tables (event types, observability tools, message queues, OpenAI-compatible tools)
- Strong workflow diagrams with clickable images
- Good featured code (EDA rulebook, API calls, survey spec, job templates)
- Effective use of callout boxes for tips, questions, and warnings
- Links to Automation Hub for every collection and tool mentioned

**Weaknesses:**
- No explicit problem statement with quantified pain
- No validation section — the guide ends at "Execute Remediation" without showing how to verify the fix worked
- Section 4 (Execute Remediation / Policy Enforcement) is essentially a stub with just a link
- Very long (~630 lines) which may overwhelm readers — could benefit from a "quick start" path
- Several minor typos: "Interference" should be "Inference" (line 117), "infrastrucure" (multiple), "componenets", double space in "Execute  Remediation"
- No maturity path / crawl-walk-run
- No explicit prerequisites section

**Suggestions:**
- Add a brief problem statement at the top
- Flesh out Section 4 (Execute Remediation) — it is the climax of the entire workflow and currently has almost no content
- Add a validation section: "How do you know it worked?"
- Add a prerequisites section listing AAP version, required collections, and external dependencies
- Fix the typos noted above
- Consider a "Quick Start" callout at the top for readers who want the TL;DR
- Add a maturity path: Manual remediation -> AI-assisted diagnosis -> AI-generated playbooks -> Fully automated self-healing

---

### 5. Configuring Ansible Lightspeed intelligent assistant with Red Hat AI Inference Server on RHEL

**Link**: https://access.redhat.com/articles/7130595
**Grade: 8 / 10**

**Strengths:**
- Extremely practical and end-to-end: GPU setup -> NVIDIA drivers -> container deployment -> AAP integration
- Clear validation step with curl test and expected output
- Good coverage of hardware options (NVIDIA and AMD)
- Provides the exact podman command with all required flags and explains each one
- Connects the deployment to AAP via OpenShift CR configuration — completes the loop

**Weaknesses:**
- Title is procedural rather than outcome-oriented
- No business framing — why should someone self-host vs. use cloud?
- No persona mapping
- No architecture diagram showing GPU host -> Inference Server -> AAP/OCP -> Lightspeed UI
- No maturity path
- Somewhat narrow scope (only RHEL + podman path; no Kubernetes/OpenShift serving option)

**Suggestions:**
- Add 1-2 sentences framing the "why": air-gapped environments, data sovereignty, cost control
- Add an architecture diagram showing the end-to-end data flow
- Cross-link to the AI Infrastructure guide (7118390) which covers the infra.ai/redhat.ai provisioning path
- Note the relationship between this guide and RHEL AI deployment — they are complementary but different entry points

---

### 6. Network Fact Gathering & Reporting - Solution Guide

**Link**: https://access.redhat.com/articles/7123361
**Grade: 6 / 10**

**Strengths:**
- Good prerequisite section with extensive learning path links for beginners
- Clear featured collections (Cisco IOS, network.backup)
- Simple, approachable code example
- Links to demos and self-paced labs
- Links to the companion Backup/Config guide as a next step

**Weaknesses:**
- Very thin — only 2 steps with minimal depth
- No architecture diagram
- No validation section (how do you verify the facts were gathered correctly?)
- Step 2 (export to reporting tool) is hand-waved with "you can export your data" — no actual code or instructions
- No business framing beyond bullet points
- No operational impact rating in the body (only "None" in overview)
- No maturity path

**Suggestions:**
- Expand Step 2 with an actual Jinja2 template example or Splunk export playbook
- Add a validation step showing expected fact output structure
- Add a simple diagram: Network Devices -> Ansible Fact Gathering -> Report/Dashboard
- Consider merging this with the Backup/Config guide since both are short and complementary
- Add a maturity path: Fact gathering -> Compliance reporting -> Drift detection -> Automated remediation

---

### 7. Network Back Up and Configuration - Solution Guide

**Link**: https://access.redhat.com/articles/7123366
**Grade: 7 / 10**

**Strengths:**
- Good structure with 3 clear steps (Backup, Configure, Restore)
- Per-step operational impact ratings (Low, Medium, High) — this is a pattern other guides should adopt
- Practical playbook examples using validated content (network.backup)
- Good warning about testing restore in dev before production
- Links to EDA network automation labs as next steps
- Lists specific Cisco IOS modules available for configuration

**Weaknesses:**
- No architecture diagram
- No explicit business framing or ROI discussion
- No validation step (how do you verify the backup was successful? How do you verify config was applied?)
- GitHub PAT setup is mentioned in prerequisites but not walked through
- No maturity path

**Suggestions:**
- Add a validation step after each operation (e.g., diff the backup file, verify VLAN creation with show commands)
- Add a simple diagram: Backup -> Git -> Config Change -> Validate -> Restore (if needed)
- Add a brief business frame: "Network misconfigurations account for X% of outages..."
- Add maturity path: Manual backups -> Scheduled automated backups -> Config drift detection -> Self-healing network

---

### 8. ServiceNow ITSM Ticket Enrichment Automation - Solution Guide

**Link**: https://access.redhat.com/articles/7127603
**Grade: N/A (subscriber-only content)**

This article is behind the Red Hat subscriber login wall. Only the title and a single overview sentence were accessible:

> *"ServiceNow is one of the most common ITSM solutions in the market. In this guide, we'll walk through a simple automation use case to help you quickly create an incident and update a ServiceNow ITSM ticket with additional information."*

**Based on the visible overview:**
- The title is good — it describes a specific operational outcome (ticket enrichment)
- The overview sentence frames the use case clearly
- Cannot assess code quality, validation, architecture, or depth without full access

**Suggestion:** If possible, ensure this article is accessible without login for broader reach, or at minimum provide a more detailed public preview.

---

## Summary Table

| # | Article | Grade | Top Strength | Top Improvement Area |
|---|---------|-------|-------------|---------------------|
| 1 | Automation Dashboard and Analytics | 8/10 | Persona mapping and step-by-step setup | Add architecture diagram and problem statement |
| 2 | Get started with EDA (Ansible Rulebook) | 8/10 | Hands-on test scenarios with expected output | Add architecture diagram and business framing |
| 3 | AI Infrastructure automation with Ansible | 7/10 | Clear end-to-end with validation | Add executive hook and operational impact |
| 4 | AIOps automation with Ansible | 7/10 | Comprehensive reference tables and diagrams | Flesh out Section 4, add validation, fix typos |
| 5 | Configuring Lightspeed with AI Inference Server | 8/10 | Practical GPU-to-AAP walkthrough | Add architecture diagram and business framing |
| 6 | Network Fact Gathering & Reporting | 6/10 | Good prerequisite learning paths | Expand thin content, add validation and export example |
| 7 | Network Back Up and Configuration | 7/10 | Per-step operational impact ratings | Add validation steps and architecture diagram |
| 8 | ServiceNow ITSM Ticket Enrichment | N/A | Clear title and framing (from preview) | Content behind login wall |

---

## Cross-Cutting Observations

**Patterns that work well across guides:**
- Linking to Automation Hub for every collection mentioned
- Providing both CLI and AAP Controller paths (IA guide, Network guides)
- Including demo/lab links alongside written content
- Per-step operational impact ratings (Network Backup guide)

**Recurring gaps across most guides:**
1. **No architecture diagrams** — Only the AIOps guide has workflow visuals. Most guides would benefit from even a simple 3-5 block flow diagram.
2. **No explicit problem statement** — Most guides start with "Background" or "Overview" without framing the business pain.
3. **Validation is inconsistent** — Some guides have it (IA, Lightspeed), many do not (AIOps, Dashboard, Network Fact Gathering).
4. **No maturity path** — Zero guides implement crawl/walk/run despite the best practices doc advocating for it.
5. **No version tracking** — None specify AAP version tested, collection versions, or a "last updated" date.
6. **Typos and polish** — Several guides have minor spelling/grammar issues that could be caught with a review pass.
