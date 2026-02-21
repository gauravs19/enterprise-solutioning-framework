# Strategist Blueprint: The "Core vs. Context" Buy-Build-Partner Framework

**Purpose:** To decide whether an enterprise should invest in custom engineering, license a product, or leverage a strategic partnership.

---

## 1. The Decision Matrix (Geoffrey Moore's Framework)

We evaluate every project based on two axes: **Business Strategic Value** vs. **Operational Mission-Criticality.**

### Quadrant 1: MISSION CRITICAL + STRATEGIC (BUILD)
*   **Definition:** These are the "Crown Jewels." The capabilities that provide a unique competitive advantage (e.g., a proprietary AI maintenance algorithm for Hitachi turbines).
*   **Strategy:** **Build & Own.** Insource the engineering. Patent the logic. These are your "Differentiators."

### Quadrant 2: MISSION CRITICAL + NON-STRATEGIC (BUY/PARTNER)
*   **Definition:** The system MUST work for the business to run, but it doesn't make you "better" than your competitor (e.g., The HR Payroll system or the Message Broker).
*   **Strategy:** **Buy & Configure.** Use industry standards (e.g., Salesforce, Azure Service Bus). Focus on integration, not invention.

### Quadrant 3: NON-CRITICAL + STRATEGIC (PARTNER/INCUBATE)
*   **Definition:** Future-looking experiments or "Nice-to-haves" that could become strategic (e.g., An experimental Blockchain for supply chain trace).
*   **Strategy:** **Partner or Outsource.** Minimize internal burn while testing market fit.

### Quadrant 4: NON-CRITICAL + NON-STRATEGIC (ELIMINATE/COMMODITIZE)
*   **Definition:** Legacy systems or administrative tools.
*   **Strategy:** **SaaS or Managed Service.** Minimize TCO (Total Cost of Ownership).

---

## 2. The TCO (Total Cost of Ownership) Reality Check

When choosing "BUILD," the Architect must account for the **Hidden 70%** of the cost:

| Component | BUY (Managed Service) | BUILD (Custom Engineering) |
| :--- | :--- | :--- |
| **Initial Cost** | High (License/Subscription) | Moderate (Dev Sprints) |
| **Maintenance** | Included in SLA | High (Security patches, Library updates) |
| **Upgrade Path** | Vendor-driven | Internal Roadmap dependency |
| **Expertise** | Widespread in market | Niche/Project-specific knowledge |
| **Opportunity Cost** | Low | High (Engineers NOT building Tier 1 apps) |

---

## 3. Decision Heuristics
*   **The 80/20 Rule**: If a COTS (Commercial Off-The-Shelf) product meets 80% of requirements with < 20% customization, **BUY**.
*   **The Latency Test**: If the requirement needs < 10ms response time and no local product supports it, **BUILD**.
*   **The Talent Pool**: If you cannot hire 5+ maintainers for the custom stack in the current market, **DO NOT BUILD**.

---
*Created by Gaurav Sharma — Solutions Architect Frameworks*
