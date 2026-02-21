# The Senior Architect's Reliability Checklist (NFR Audit)

**Version:** 4.0 (Enterprise Industrial IoT & GenAI focus)
**Purpose:** A final gatekeeper review before a system is moved from UAT (User Acceptance Testing) to Production.

---

## Pillar 1: High Availability & Fault Tolerance
- [ ] **Circuit Breakers**: Are all external API calls wrapped in resilience patterns (e.g., Resilience4j/Hystrix)?
- [ ] **Retries & Backoff**: Do retry loops use "Exponential Backoff with Jitter" to prevent Thundering Herd problems?
- [ ] **Data Redundancy**: Is the database configured for Multi-AZ (Availability Zone) with < 30s failover?
- [ ] **Broker Resilience**: Does the message broker (Kafka/Redis) have a persistent disk and ACK requirements?

## Pillar 2: Scalability & Performance
- [ ] **Horizontal Scaling**: Are all application services 100% stateless? (No local session storage).
- [ ] **Database Connection Pooling**: Are connection limits tuned for peak load?
- [ ] **Caching Strategy**: Are we using TTL (Time-to-Live) and Eviction policies to prevent memory leaks?
- [ ] **Cold Start Management**: For Serverless/K8s, is there a "warm-up" strategy for peak events?

## Pillar 3: Observability (The "SRE" Pillar)
- [ ] **Traced Context**: Is a `Correlation-ID` passed through every service boundary for distributed tracing?
- [ ] **Standardized Logs**: Are logs formatted as JSON for ingestion into ELK/Splunk?
- [ ] **Critical Alerts**: Are thresholds defined for 4xx/5xx errors, P99 latency, and disk/memory saturation?
- [ ] **Semantic Metrics**: Do we measure "Business Success" (e.g., "Turbines Managed") vs just "Technical Success" (e.g., "CPU %")?

## Pillar 4: Security Pillar (Zero-Trust)
- [ ] **Secret Management**: Are there ZERO hardcoded keys? (Using Hashicorp Vault/AWS Secrets Manager).
- [ ] **Token Validation**: Are JWTs/Tokens validated locally at the Gateway and internally at the Service?
- [ ] **PII/Sensitive Data**: Is data encrypted at rest and masked in logs?
- [ ] **Supply Chain Security**: Are all Docker images and Maven/PyPI packages scanned for CVEs?

## Pillar 5: GenAI Resilience (New)
- [ ] **Prompt Governance**: Is there a layer to prevent prompt injection and PII leakage?
- [ ] **Hallucination Gates**: Does the RAG pipeline have a "groundedness" check before outputting results?
- [ ] **LLM Fallback**: If the primary LLM (e.g., GPT-4) is down, is there a secondary fallback (e.g., Llama/Claude)?
- [ ] **Token Budgeting**: Is there a rate-limiter per user/tenant to prevent cost spikes?

---
*Created by Gaurav Sharma — Solutions Architect Frameworks*
