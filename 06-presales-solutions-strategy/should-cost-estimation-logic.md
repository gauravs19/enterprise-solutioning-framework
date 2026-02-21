# Should-Cost Estimation Logic for Enterprise Solutions

**Context:** During the presales phase, the most common question is: "How much will this cost to build and run?"

---

## 1. The 3-Point Estimation Method
To account for uncertainty, we provide three figures:

1.  **Optimistic (The "Happy Path")**: Assumes perfect data quality and zero infra hurdles.
2.  **Pessimistic (The "Legacy Reality")**: Accounts for data silos, security bottlenecks, and stakeholder delay.
3.  **Most Likely**: The weighted average used for the actual pitch.

---

## 2. The "NFR Tax"
Junior engineers estimate "Functions." Senior architects estimate "Quality."

Every feature estimate should include the "NFR Tax" (Non-Functional Requirements):
*   **Unit/Integration Tests**: +20%
*   **Observability/Instrumentation**: +10%
*   **Security Hardening**: +10%
*   **Documentation & Onboarding**: +10%

**Total Multiplier:** 1.5x of the raw "coding time."

---

## 3. The Run-Cost Projection
Presales must prove the solution is sustainable.
*   **Infrastructure Estimate**: AWS/Azure pricing calculator output.
*   **Support & Operations**: Projected L2/L3 support hours per month.
*   **Technical Debt Budget**: Allocating 15% of the annual budget for ongoing refactoring.

---
*Created by Gaurav Sharma — Product & Solutions Leadership*
