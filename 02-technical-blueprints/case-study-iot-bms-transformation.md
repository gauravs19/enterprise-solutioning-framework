# Case Study: Multi-Tenant BMS Transformation (100K+ Devices)

**Client Context:** A global real-estate leader with 4,000+ buildings.
**Problem:** Data siloed in local building gateways. No central visibility across regions. 15% energy waste due to unoptimized cooling.

---

## 1. The Solution Architecture

### Data Ingestion Logic
*   **The Problem:** Traditional "Polling" architectures crashed the central hub when more than 1,000 buildings were integrated.
*   **The Fix:** Migrated to a **Decoupled Push Architecture** using MQTT and Redis Streams. Reduced hub CPU saturation by 60%.

### Multi-Tenancy Strategy
*   **Schema-per-Tenant**: Used to ensure that "Client A" (e.g., a Pharmaceutical tenant) could never see the environmental data of "Client B" (e.g., a Banking tenant) sharing the same building.

---

## 2. Technical Outcomes
*   **Scalability**: Proven to handle bursts of 20,000 events/second during grid demand-response events.
*   **Availability**: 99.95% uptime achieved through Multi-AZ regional failover.
*   **Cost Optimization**: Reduced cloud storage costs by 45% by implementing a **"Telemetric Decay" policy** (High-res data kept for 7 days, 1-min aggregations kept for 12 months).

---

## 3. Business Impact
*   **Energy Savings**: $1.2M USD saved across the portfolio within the first year.
*   **Operational MTTR**: Reduced mean-time-to-repair for HVAC systems by 22% through predictive labeling.

---
*Created by Gaurav Sharma — Solutions Architect Frameworks*
