# Iteration 2

## Step 2: Iteration Goal

### Main Functionality
- UC-1: Query Assistant
- UC-2: Notifications
- UC-3: Schedule Manager
- UC-7: Data Sync Services

---

## Step 3: Elements to Refine from Iteration 1
- User Interaction Layer (presentation layer modules)
- Business Logic Services (application/service modules)
- Data Sync & Integration Layer (integration/data interface layers)
- System Operations Layer (operation modules)

---

## Step 4: Design Concepts

| Design Decision | Rationale |
|-----------------|-----------|
| Adopting a Layered Architecture across UI, Business Logic, Integration and Operation layers | Layered system structure provides a clear separation of concerns, which simplifies responsibilities. This supports modifiability, making sure that each major area can work independently. A monolithic design would result in an increase in coupling which would cause dependencies. |
| Service Based Decomposition within Business Logic | Decomposing core functionality into service modules will support AIDAPS use cases, while maintaining independence among important functional elements. |
| External System Connectors in Integration Layer | Specialized connectors like the LMSConnector isolate system dependencies allowing for architecture to adapt to changes in external university systems. Without this there would be an increase in coupling and a decrease in modificability. |
| Centralized System within Operations Layer | Monitoring, health checking, deployments and update management should be uniformly handled across all subsystems. A fragmented approach would result in inconsistent operational behaviour which is harder to control. |

---

## Step 5: Instantiate Architectural Elements

| Design Decision & Location | Rationale |
|----------------------------|-----------|
| Make initial domain model for AIDAP | Setting a domain model early on helps identify the core concepts that are implemented across the key use cases that represent the main functionality. An initial model is created at this stage so that it can evolve in later iterations. |
| Map the use cases to domain objects | Domain objects and key use cases are associated together to ensure that the essential responsibilities that make the system functional are represented. This prevents missing out on important behaviour. |
| Splitting of domain objects across major architectural layers | The separation of domain objects across the UI, business logic, integration and operations layers provides clarity on which layer holds what responsibility. This establishes a structured approach to complex interfaces, preventing dependency. |
| Identify layer specific modules with clear interfaces | The modules group the systems main responsibilities like handling queries, notifications, data syncing and system operations. Clear interfaces support independence of the system for future updates. |
| Introduce connector abstractions for external systems | Abstracting LMS, and other subsystems into connector components isolates AIDAP from external API modifications. This lowers integration risk, maintaining stability should external systems evolve. |
| Establish operational modules for runtime support | Defining the systems operation modules ensure the system operates smoothly and deployment activities are coordinated across all layers. This helps in prevention of fragmented operational logic. |

---

## Step 6
Domain Model Diagram
<img width="1701" height="960" alt="image" src="https://github.com/user-attachments/assets/684fcff6-130d-4c63-a470-dc1b003d1bcd" />

Sequence Diagram (Query Assistant)
<img width="1134" height="672" alt="image" src="https://github.com/user-attachments/assets/2ddd1883-a6f5-403d-b067-a0c33f5c56c0" />

---

## Step 7: Scenario Analysis

| Scenario | Status | Design Decision Made |
|----------|--------|-----------------------|
| UC-1 Query Assistant | Completely Addressed | Domain objects were defined and were correlated with UC-1. The queryAssistantService uses these objects and the chat calls it using an interface. |
| UC-2 Notifications | Completely Addressed | Notifications were added in the domain model and the notification service was addressed in the business layer. |
| UC-3 Schedule Manager | Completely Addressed | Course and scheduleItem were created, fulfilling UC-3. Schedule UI displays course and scheduleItem objects. |
| UC-7 Data Sync Services | Completely Addressed | External systems were introduced along with dataSyncService which works specifically to coordinate domain objects. |
| QA-5 Interoperability | Completely Addressed | All external interactions have to go through a connector such as LMSConnectors or RegistrationConnectors. |
| QA-6 Modifiability | Partially Addressed | Layered Architecture was used allowing for clear modular interfaces. Could be refined in more detail. |
| QA-2 Availability | Partially Addressed | DataSyncService and connectors to external systems keep the data in sync and avoid replication. |
