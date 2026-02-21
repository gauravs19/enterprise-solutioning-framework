# Master Framework: The Senior Architect’s Reliability & NFR Audit

**Classification:** Architectural Quality Assurance  
**Target Domains:** Mission-Critical Cloud-Native Systems, Industrial IoT, Financial Gateways  
**Version:** 4.2 (Chaos-Engineering & SRE Optimized)

---

## 🏛️ Executive Abstract
In the enterprise lifecycle, most systems fail not because of incorrect business logic, but because of poor **Non-Functional Requirement (NFR)** planning. A system that is 100% accurate but 0% available is a failure. 

This checklist serves as the **Final Gatekeeper** for senior architects, technical leads, and SRE managers. It defines the "Production-Ready" bar for systems handling high-concurrency, high-value data. It moves beyond simple "Yes/No" questions to provide technical rationale for each audit point.

---

## 🏗️ Pillar 1: High Availability (HA) & Fault Tolerance
High availability is not a "Feature"; it is an **Architectural Commitment**.

1.  **Redundancy & Multi-AZ Topology**
    - [ ] **Audit Requirement:** Does the application run in at least three Availability Zones (AZs) with automated traffic shifting?
    - [ ] **Rationale:** A single-AZ failure (e.g., AWS `us-east-1a` outage) should be a non-event for the business.
2.  **Statelessness & Session Management**
    - [ ] **Audit Requirement:** Are all application nodes 100% stateless? Are local sessions or in-memory caches (Sticky Sessions) strictly prohibited?
    - [ ] **Rationale:** Statelessness allows for the "Cattle not Pets" approach—where any node can be terminated and replaced without user impact.
3.  **Circuit Breaker Implementation (Bulkheads)**
    - [ ] **Audit Requirement:** Are all downstream API calls wrapped in Circuit Breakers (e.g., Resilience4j, Istio Envoy)?
    - [ ] **Rationale:** Prevents "Cascading Failures." If a third-party SMS provider is down, the whole checkout system should not hang.
4.  **Exponential Backoff with Jitter**
    - [ ] **Audit Requirement:** Do all retries use a random "Jitter" factor?
    - [ ] **Rationale:** Prevents the **Thundering Herd** problem. If 10,000 devices reconnect at the exact same millisecond after an outage, they will DDoS your internal load balancer.
5.  **Data Persistence Quorums**
    - [ ] **Audit Requirement:** For Redis/Kafka/DBs, is a quorum-based ACK or replication factor of at least 3 configured?
    - [ ] **Rationale:** Protects against "Split Brain" scenarios and data loss during node reboots.

---

## 🚦 Pillar 2: Scalability & Performance Density
Scalability is the ability to handle growth; **Performance Density** is the ability to do it cost-effectively.

1.  **Connection Pooling & Resource Limits**
    - [ ] **Audit Requirement:** Are DB connection pools, thread pools, and file descriptor limits explicitly tuned and monitored?
    - [ ] **Rationale:** Most systems crash because they "Run out of connections" long before they run out of CPU.
2.  **Horizontal Pod Autoscaling (HPA)**
    - [ ] **Audit Requirement:** Are scaling triggers based on a mix of CPU, Memory, and **Custom Metrics** (e.g., Queue Depth)?
    - [ ] **Rationale:** Scaling on CPU alone is insufficient for I/O bound ingestion engines.
3.  **Caching Strategy & Eviction**
    - [ ] **Audit Requirement:** Does every cache have a defined TTL (Time-to-Live) and an LRU (Least Recently Used) eviction policy?
    - [ ] **Rationale:** Prevents "Memory Leak" incidents where stale data consumes the entire RAM heap.
4.  **Database Index & Partitioning Audit**
    - [ ] **Audit Requirement:** For any table > 10M rows, is there a partitioning strategy (e.g., by `tenant_id` or `created_at`)?
    - [ ] **Rationale:** Long-term table growth leads to exponential query degradation without partitioning.

---

## 🔍 Pillar 3: Observability (The "SRE" Pillars)
Observability is the ability to understand the internal state of a system purely through its external outputs.

1.  **Distributed Tracing (Tracing-by-Default)**
    - [ ] **Audit Requirement:** Is a `trace_id` propagated across every service boundary (OpenTelemetry)?
    - [ ] **Rationale:** In a microservices mesh, you cannot debug a "Slow Request" without a unified trace across 5 disparate services.
2.  **Standardized Structured Logging**
    - [ ] **Audit Requirement:** Are all logs emitted as JSON with standard fields (`level`, `service`, `trace_id`, `tenant_id`)?
    - [ ] **Rationale:** Human-readable logs are useless for automated alerting and centralized log aggregation logic.
3.  **The Four Golden Signals (Core Dashboard)**
    - [ ] **Audit Requirement:** Do we have dashboards for **Latency, Traffic, Errors, and Saturation**?
    - [ ] **Rationale:** These are the minimum data points required to detect 95% of operational incidents.
4.  **Semantic Alerting (Anti-Alert Fatigue)**
    - [ ] **Audit Requirement:** Are alerts based on **Symptoms** (e.g., "Success Rate < 95%") rather than causes (e.g., "CPU > 80%")?
    - [ ] **Rationale:** If your CPU is at 90% but the application is performing perfectly, you shouldn't wake an engineer at 3 AM.

---

## 🛡️ Pillar 4: Zero-Trust Security & Governance
Security is no longer a "Moat"; it is an individual identity for every packet.

1.  **Secret Management (No-Hardcode Policy)**
    - [ ] **Audit Requirement:** Are zero credentials stored in Repo, Env variables, or Docker images? (Using Vault/KeyVault).
    - [ ] **Rationale:** Prevents lateral movement after a developer machine or registry compromise.
2.  **Mutual TLS (mTLS) Mesh**
    - [ ] **Audit Requirement:** Is service-to-service communication encrypted and mutually authenticated?
    - [ ] **Rationale:** Protects against "Man-in-the-middle" attacks within the internal VPC.
3.  **PII Sanitization & Data Masking**
    - [ ] **Audit Requirement:** Is sensitive data (Emails, Names, IDs) masked in logs and non-production DBs?
    - [ ] **Rationale:** Prevents accidental data leakage to developers or support staff viewing log dashboards.
4.  **Supply Chain Integrity**
    - [ ] **Audit Requirement:** Are all base images and dependencies scanned for CVEs in the CI/CD pipeline?
    - [ ] **Rationale:** 80% of security vulnerabilities enter the system through third-party libraries (Maven/PyPI).

---

## 🤖 Pillar 5: GenAI Resilience (Modern Add-on)
Building with LLMs requires a new class of "Intelligence NFRs."

1.  **Hallucination Gates (Groundedness Checks)**
    - [ ] **Audit Requirement:** Does the RAG pipeline include a programmatic "Fact-Check" against the source document?
    - [ ] **Rationale:** Prevents the AI from giving "Confident but Wrong" maintenance instructions.
2.  **Token Budgeting & Rate Limiting**
    - [ ] **Audit Requirement:** Are there "Per-Tenant" limits on LLM token consumption?
    - [ ] **Rationale:** Protects the company from a $10k cloud bill caused by a "Recursive Loop" in an agent's reasoning.
3.  **LLM Redundancy (Model Fallback)**
    - [ ] **Audit Requirement:** Can the system switch from GPT-4 to Claude or Llama if the primary API is down?
    - [ ] **Rationale:** OpenAI/Anthropic APIs are not 100% available; your business capability shouldn't depend on a single third-party vendor.

---

## 🚀 The Auditor’s Scoring Logic
Evaluate each pillar on a scale of 1-5:
*   **5 (Production Elite):** Complete automation, chaos-tested.
*   **3 (Enterprise Minimum):** Secure and scalable, but requires manual intervention during recovery.
*   **1 (Development Quality):** High risk of data loss and downtime.

**The "SRE Rule":** No system may be promoted to Production with a score of < 4 in Security or High Availability.

---
*Created by Gaurav Sharma — Solutions Architect Frameworks*
