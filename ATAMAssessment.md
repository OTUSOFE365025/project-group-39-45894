# Project Assessment

## 1. ATAM Risk Assessment Table

| Scenario / Quality Attribute                                             | Architectural Decision                                                         | Risks (R)                                                                                              | Non-Risks (NR)                                                                                                           | Sensitivity Points (S)                                                                                              | Tradeoffs (T)                                                                                                                     |
|--------------------------------------------------------------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **QA-2 – Availability** (Failure occurs on a node during peak times)     | Added a **LoadBalancer** and replicas of nodes along with health checks      | **R1** – If health checks are inaccurate or slow, the failover mechanism might not trigger in time    | **NR1** – Replicas of nodes can guarantee that the system will stay alive as long as at least one node is active        | **S1** – The frequency of health checks will have a large impact on fail-detection speed                            | **T1** – More frequent checking can improve availability but increases operational overhead                                     |
| **QA-3 – Security** (Admin accesses restricted functionality)            | Added an **AuditLogService** that stores activity logs                       | **R2** – If the log grows too large there can be delays that might affect performance                 | **NR2** – User actions become traceable, improving accountability and addressing privacy concerns                      | **S2** – The quantity of logged events may impact system latency                                                    | **T2** – Increased storage use and slower performance in exchange for improved security                                          |
| **QA-7 – Consistency** (External LMS or Registration becomes unavailable or outdated) | Added **retry logic** and **short-term caching**                              | **R3** – Large amounts of retries may overload other operations and cause delays                      | **NR3** – Cache ensures that the UI remains responsive even if the external systems fail                               | **S3** – Retry count and timeout length can affect consistency between the main system and the LMS                 | **T3** – Numerous retries can improve consistency but reduce system performance when retrying                                |

---

## 2. Description of Risks, Non-Risks, Sensitivity Points, and Tradeoffs

### 2.1 Risks

- **R1 – Slow or inaccurate health checks**  
  → Delay failover and reduce availability.

- **R2 – Audit log storage growth may impact performance**  
  → High logging volume may affect database write speed.

- **R3 – Aggressive retry may cause overloads during downtimes**  
  → Repeated retries during LMS or Registration downtime may cause sequential errors.

### 2.2 Non-Risks

- **NR1 – Redundant nodes maintain uptime/availability**  
  → Replicas along with a load balancer satisfy QA-2’s requirement of staying online.

- **NR2 – Audit logs ensure traceability**  
  → Satisfies privacy requirements and QA-3 by ensuring accountability for users.

- **NR3 – Short-term caching ensures UI responsiveness**  
  → Allows users to avoid visible failures during external system outages.

### 2.3 Sensitivity Points

- **S1 – Frequency of health checks**  
  → Higher frequency means quicker failover and less downtime.

- **S2 – Logged modules / log detail**  
  → More fields captured in logs can slow database writes but improve security and traceability.

- **S3 – Retry count**  
  → Directly affects the consistency between AIDAP and external systems.

### 2.4 Tradeoffs

- **T1 – Overhead (–) vs. Availability (+)**  
  → More frequent checks lead to higher computational overhead.

- **T2 – Performance (–) vs. Logging Security (+)**  
  → More detailed audit logs slow operations but improve privacy and security.

- **T3 – System Load (–) vs. Retry Count (+)**  
  → Higher retry count improves consistency with external systems but worsens performance.

---

## 3. Utility Tree

<img width="758" height="437" alt="image" src="https://github.com/user-attachments/assets/c1f0a06c-b890-4fad-bd8c-ce98e4d1b65b" />

