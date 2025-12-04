# Iteration 3

---

## Step 2: Establish Iteration Goal by Selecting Drivers

For this iteration, the goal is to improve on the following quality attributes:

- **Availability (QA-2)**
- **Security/Privacy (QA-3)**
- **Consistency (QA-7)**

This will ensure that the system will have quick recovery time from failure as well as maintaining uptimes.  
Data within the system should remain synchronized across all connected systems, while ensuring secure traceable access.

---

## Step 3: Choose One or More Elements of the System to Refine

| **System Element** | **Enhancements and Responsibilities** |
|---------------------|---------------------------------------|
| **Systems Operation Layer** | - Enhanced to include failure detection, regular health checks, and logging services.<br>- Supports alerting, zero-downtime deployment, and recovery processes.<br>- Includes monitoring services that collect real-time metrics from each component.<br>- Adds an audit log that stores user and system activity received from the business logic layer. |
| **Business Logic Services Layer** | - `QueryAssistantService`, `NotificationService`, and `DataSyncService` upgraded to produce detailed and organized logs per user/system interaction.<br>- Data passed to the operations layer for secure storage. |
| **Integration Layer** | - `LMSConnector`, `RegistrationConnector`, and `CalendarConnector` improved with retry logic for failures.<br>- Temporary caching introduced to improve consistency among user interfaces during downtime. |

---

## Step 4: Choose One or More Design Concepts That Satisfy the Selected Drivers

| **Design Concept and Location** | **Rationale** |
|----------------------------------|----------------|
| Include redundancy and health check mechanisms | Several AIDAP nodes will simultaneously run behind a load balancer. In the event of a node failure detected through a health check, the systems operations layer will automatically reroute requests. This maintains **availability (QA-2)** with zero-downtime. |
| Implement monitoring services for operation metrics | The monitoring service collects real-time data on error rates, uptime, and latency from each component. Supports fault detection and recovery by providing alerts to maintainers, enhancing **availability and consistency (QA-2, QA-7)**. |
| Add Audit Log Service for user and system activity | Tracks every user and service interaction from the business layer, identifying who performed what action and when. Strengthens **security/privacy (QA-3)** by ensuring all activity is traceable. |
| Apply retry and timeout control in connectors | Integration layer uses retry and timeout mechanisms to handle slow or failed responses from external systems, preventing blocking of core services. |
| Enable temporary caching for user data consistency | During downtime, integration layer uses short-term caching to continue serving users with recent data, improving **consistency (QA-7)**. |
| Establish centralized alerting and recovery processes | When monitoring detects a failure, system operation modules trigger automated alerts and switch to replicas, ensuring **availability (QA-2)**. |

---

## Step 5: Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces

| **Element** | **Responsibility** |
|--------------|--------------------|
| **LoadBalancer** | Distributes requests across AIDAPNode instances. Works with the MonitoringService to ensure routing only to healthy nodes, maintaining high availability. |
| **MonitoringService** | Collects metrics from all components and generates alerts for maintainers when intervention is required. |
| **AuditLogService** | Receives structured, detailed logs from Business Logic Services for secure auditing and traceability. Enhances system security. |
| **SystemOperationsModule** | Performs health checks and coordinates recovery between LoadBalancer and MonitoringService. Automatically reroutes to working nodes upon failure detection. |
| **CacheManager** | Stores temporary copies of user data if external systems fail, maintaining responsiveness and consistent dashboards. |
| **Connectors (LMS, Registration, Calendar)** | Execute retry and timeout controls for external systems. Use cached data during downtime to maintain stability and performance. |

---

## Step 6: Refined Deployment Diagram
<img width="498" height="795" alt="image" src="https://github.com/user-attachments/assets/45c2b7c9-6428-452b-aa1c-a4fbab1c9cff" />


---

## Step 7: Perform Analysis of Current Design and Review Iteration Goal

| **Quality Attribute / Constraint** | **Not Addressed** | **Partially Addressed** | **Completely Addressed** | **Design Decision Made During the Iteration** |
|-----------------------------------|:-----------------:|:-----------------------:|:------------------------:|----------------------------------------------|
| **QA-2 Availability** |  |  | ✔ | Implemented AIDAPNode replicas running behind a LoadBalancer. Added regular health checks and failure detection for rerouting requests. |
| **QA-3 Auditability** |  | ✔ |  | Added AuditLogService to record detailed user and system actions from the business layer, stored securely in the operations layer. |
| **QA-7 Consistency** |  | ✔ |  | Enhanced connectors with retry and timeout mechanisms; CacheManager preserves data availability during downtime. |
| **CON-1 Secure Web Access (HTTPS)** |  |  | ✔ | No new changes from Iteration 2; remains enforced. |
| **CON-2 Authentication / SSO Integration** |  |  | ✔ | Existing login and SSO remain active; unaffected by new changes. |
| **CON-3 99.5 % Uptime Requirement** |  |  | ✔ | Backup nodes and auto-recovery maintain uptime; monitoring ensures continuous operation. |

---

