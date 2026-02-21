# Architectural Decision Record (ADR) Master Template

**Purpose:** To capture the context, rationale, and consequences of significant technical choices. This prevents "Architectural Amnesia" and informs future stakeholders.

---

## ADR XXX: [Short, Descriptive Title]

**Status:** Proposed | **Accepted** | Superseded | Deprecated
**Date:** YYYY-MM-DD
**Deciders:** [Name/Role], [Name/Role]
**Consulted:** [Team/Stakeholder]

---

### 1. Context & Problem Statement
*Describe the technical or business situation we are in. What is the specific challenge or constraint? (e.g., "Current Python-based consumer is hitting global interpreter lock (GIL) limits at 5000 msg/sec").*

### 2. Decision Drivers (The "NFRs")
*   **Driver 1**: Throughput (Needs to handle 10k+).
*   **Driver 2**: Maintainability (Team has Java skills).
*   **Driver 3**: Cost (Minimize managed service fees).

### 3. Considered Options
*   **Option 1**: [Technology X] - (e.g. Scaling Python with Multi-processing).
*   **Option 2**: [Technology Y] - (e.g. Migrating to Reactive Spring Boot).
*   **Option 3**: [Technology Z] - (e.g. Using a Managed Service like AWS Lambda).

### 4. Decision Outcome
**Chosen Option:** [Decision]

#### Rationale:
*Explain the "Why." Link to the Decision Drivers in Section 2. (e.g., "Option 2 was chosen because it provides the required throughput while leveraging existing team Java expertise, even though the initial Dev time is 20% higher").*

### 5. Consequences
*   **Positive (Benefits)**: [e.g. 5x Throughput, Improved Type Safety].
*   **Negative (Risks/Costs)**: [e.g. New infra required, Team needs to learn Project Reactor].
*   **Neutral (Follow-on work)**: [e.g. Need to update CI/CD pipelines for Java].

---

### 📝 Guidelines for ADRs:
1.  **Be Objective**: List the Cons of your chosen option honestly.
2.  **Keep it Brief**: A good ADR should be 1-2 pages of Markdown.
3.  **No Code**: Focus on the *Pattern* and *Reasoning*, leave implementation to the SDD.

---
*Created by Gaurav Sharma — Solutions Architect Frameworks*
