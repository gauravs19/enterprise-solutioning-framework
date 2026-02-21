# Architectural Decision Record (ADR) Master Template

**Purpose:** To capture the context, rationale, and consequences of significant technical choices. This prevents "Architectural Amnesia" and informs future stakeholders.

---

## ADR XXX: [Short, Descriptive Title]

**Status:** Proposed | **Accepted** | Superseded | Deprecated
**Date:** YYYY-MM-DD
**Deciders:** [Name/Role], [Name/Role]
**Consulted:** [Team/Stakeholder]

# Master Template: Architectural Decision Record (ADR) 3.0

**Classification:** Architectural Governance & Institutional Memory  
**Applied Contexts:** Engineering Leadership, Strategic System Evolution, Knowledge Management  
**Version:** 3.2 (Markdown & Git-Native)

---

## 🏛️ Executive Abstract: Documenting the "Why"
In the lifecycle of a long-lived software project, code tells you **"What"** was built, but it rarely tells you **"Why."** Three years from now, a new architect will look at a choice—such as using Redis Streams instead of Kafka—and call it a mistake because they don't understand the constraints (Time, Cost, Talent) that existed at the time the decision was made.

The **Architectural Decision Record (ADR)** is a short text file that captures a significant architectural decision, including its context and the consequences after the decision is made. In the ESAF, ADRs are **Git-managed**, ensuring that the history of the design is as traceable as the history of the code.

---

## 🏗️ The Anatomy of a Perfect ADR

### 1. Metadata (The Header)
*   **ID:** A sequential number (e.g., `ADR-004`).
*   **Title:** A concise description of the choice (e.g., "Chosing gRPC for Internal Service-to-Service Communication").
*   **Status:** (Proposed / Accepted / Superceded / Deprecated).
*   **Owner:** The Lead Architect driving the decision.

### 2. Context (The "Forces" at Play)
This is the most critical section. Describe the environment, the constraints, and the problem you were trying to solve.
*   *Example:* "Our current REST APIs are experiencing 40% serialization overhead during peak telemetry bursts. We need a more efficient binary protocol that supports strict schema enforcement."

### 3. Options Considered
List at least 2-3 alternatives. A decision without an alternative is not a decision; it's a command.
*   **Option A:** (e.g., gRPC over HTTP/2).
*   **Option B:** (e.g., Avro over Kafka).
*   **Option C:** (e.g., Optimized REST/JSON with Gzip).

### 4. Trade-off Analysis (The "Evidence")
Evaluate each option against your project's **Primary Drivers**. Use a +/- format.
*   **Option A Pros:** High performance, built-in client generation.
*   **Option A Cons:** Requires HTTP/2 support in all load balancers; harder to debug via standard browser tools.

### 5. Final Decision
State the choice clearly and definitively. 
*   *The "Why":* "We have chosen Option A (gRPC) because the performance increase (4x throughput) outweighs the operational cost of upgrading our ELBs to support HTTP/2."

### 6. Consequences (The "Day 2" Reality)
What happens next? Document both the **Positive** and **Negative** impacts.
*   *Positive:* Reduced latency, strongly typed contracts.
*   *Negative:* All internal teams must now learn Protobuf; additional complexity in the CI/CD pipeline for stub generation.

---

## 🔍 Deep Dive: Status Workflows & Lifecycle
ADRs are living documents. 
*   **Proposed:** The idea is currently being debated in a "RFC" (Request for Comments) phase.
*   **Accepted:** The decision is final and implementation has started.
*   **Superceded:** A newer ADR (e.g., `ADR-022`) has replaced this one. Cross-link them! This prevents developers from following outdated patterns.
*   **Deprecated:** The technology or pattern is being removed from the system.

---

## 🚦 ADR Governance: When to Write One?
Not every choice needs an ADR. Use the **"One-Year Test"**:
*   "Will a developer joining the team one year from now be confused by this choice?" 
*   "Would it be difficult to reverse this decision in 6 months?"
*   *If yes to either, write an ADR.*

**Common ADR Topics:**
*   Tech Stack selection (Language, Database, Broker).
*   Security Patterns (OIDC vs SAML).
*   Communication Patterns (Sync vs Async).
*   Infrastructure Strategy (Serverless vs K8s).

---

## 📋 Sample ADR: Choosing Redis Streams for "Scale-First" Ingestor

**ID:** ADR-005  
**Title:** Using Redis Streams as the Ingestion Buffer  
**Status:** Accepted  

### Context
The `scale-first-ingestor` must handle bursts of 20,000 events/second. Our team consists of 3 Python developers. We have a total budget of $500/month for development infrastructure. We need a persistent, consumer-group capable broker.

### Options Considered
1.  **Apache Kafka:** The industry standard for high-volume streams.
2.  **Redis Streams:** Native stream type in Redis 5.0+.
3.  **RabbitMQ:** Traditional pub-sub broker.

### Trade-offs
*   **Kafka:** (+) Infinite scale. (-) High operational overhead; requires Zookeeper/KRaft; too expensive for a $500/month project.
*   **Redis Streams:** (+) We already use Redis for caching (Zero extra infra); Extremely fast (Low latency); Easy to learn. (-) Hard limit on memory; not suitable for PB-scale data.

### Decision
We have chosen **Redis Streams**.

### Rationale
Our current scale (20k RPS) fits easily into a single Redis node's memory. The operational simplicity allows our small team to focus on the business logic rather than broker maintenance.

### Consequences
*   We must implement a **"Memory Guard"** in the worker to ensure the stream doesn't grow indefinitely (`XADD MAXLEN`).
*   If we hit 100k RPS, we will need to revisit this decision (ADR-005 will be Superceded).

---

## 🏁 Architectural Summary
The Architectural Decision Record is the most powerful tool for **Reducing Technical Debt**. It forces architects to be honest about their choices, exposes "Shadow Decisions" to the light of peer review, and ensures that the system's "IQ" stays within the organization even after the lead architect leaves.

---
*Authored by Gaurav Sharma — Solutions Architect Frameworks*
