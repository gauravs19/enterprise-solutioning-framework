# Technical Debt Classification & Interest Matrix

**Purpose:** To provide Product Managers and Engineering Leads with a common language to prioritize maintenance vs. features.

---

## 1. Debt Types

| Type | Description | Consequences | Priority |
| :--- | :--- | :--- | :--- |
| **Deliberate** | We took a shortcut to hit a market deadline. | Known risks, documented workarounds. | **High** |
| **Accidental** | New patterns emerged that made our 2-year-old code obsolete. | Degrading performance, harder to hire for. | **Medium** |
| **Complexity** | The product grew features faster than the architecture could refactor. | "Spaghetti" code, high risk of regressions. | **Critical** |
| **Bit-Rot** | Libraries and JREs went out of support. | Security vulnerabilities. | **Immediate** |

---

## 2. Calculating the "Interest Rate"
The "Interest" is the time lost by developers wrestling with the debt.

*   **Interest Rate = (Estimated Sprint Velocity with Debt) / (Projected Velocity if Refactored)**
*   If your interest rate is < 0.7, your product is "Technical Bankrupt."

---

## 3. The "Refactor or Replace" Decision
*   **Refactor**: If the domain logic is still valid but the implementation is sloppy.
*   **Replace**: If the underlying architecture cannot support the current product vision (e.g., Monolith to Microservices).

---
*Created by Gaurav Sharma — Product & Solutions Leadership*
