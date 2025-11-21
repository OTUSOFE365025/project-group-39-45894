# Iteration 1

## Step 1: Selecting and Refining  Architectural Drivers

| **Category** | **Details** |
|-------------|-------------|
| **Main use cases (from phase 1)** | UC-1 - Query Assistant <br> UC-2 - Notifications <br> UC-5 - Alerts/Announcements <br> UC-6 - System Operations <br> UC-7 - Data synchronization services |
| **Quality attribute drivers** | QA-1 Performance <br> QA-2 Availability <br> QA-3 Security/Privacy <br> QA-4 Scalability <br> QA-5 Interoperability <br> QA-6 Modifiability |
| **Constraints** | CON-1 Concurrency <br> CON-2 SSO <br> CON-3 Standard API Interaction (REST/GraphQL) <br> CON-4 Cloud-native <br> CON-5 Availability <br> CON-6 Accessibility |
| **Architectural Concerns** | CRN-1 Continuous Deployment <br> CRN-2 Consistency <br> CRN-3 Efficiency <br> CRN-4 Monitoring/Metrics <br> CRN-5 Scalability <br> CRN-6 Cross-platform |

---

## Step 2: Establish the Iteration Goal 

The goal of this iteration is to establish an overall architecture for the AIDAP system. There are multiple drivers that can influence the general structure of this system’s architecture. The following drivers are those that can have a large impact:

**Quality Attributes:**

- QA-1 Performance  
- QA-2 Availability  
- QA-3 Security/Privacy  
- QA-4 Scalability  
- QA-5 Interoperability  
- QA-6 Modifiability  

**Constraints:**

- CON-1 Support of 5000 concurrent users  
- CON-2 User authentication through SSO  
- CON-3 Standard API Interaction (REST/GraphQL)  
- CON-4 System deployment must be cloud-native  
- CON-5 Must be available 99.5% of the time  
- CON-6 Accessible to different people and devices  

---

## Step 3: Choose one or more elements to refine

- Overall AIDAP system (Users and external systems)  
- User interaction layer (Chat and dashboard)  
- Notifications/Event Processing (Query assistant and notifications)  

---

## Step 4: Choose Design Concepts that Satisfy the Drivers

| **Design Concept** | **Rationale** |
|--------------------|---------------|
| Layered Architecture | This supports modifiability (QA-6) which works by separating concerns. This allows for updates to UI, logic or integrations to occur independently. |
| REST-based integration layer | Required to integrate with the learning management system, registration and calendar system. This ensures interoperability (QA-5) and retry logic for availability (QA-2). |
| Event Driven Messaging/ Message Queue | This supports performance (QA-1) and scalability (QA-4) through the process of decoupling alerts, notifications and syncing events.  Asynchronous operations can occur for notifications (UC-2) and alerts (UC-5). |
| Zero Downtime Deployment | By allowing uninterrupted updates and maintenance to the system, this supports availability (QA-2), and systems operations (UC-2). |
| API Gateway + Sign in Authentication | Focuses around access control and supports security/privacy (QA-3). This ensures that all user roles, students, lectures, administrators and maintainers can access only the features they have access to. |

---

## Step 5:  Instantiate Architecture Elements:

| **Design Decision and Location** | **Rationale** |
|----------------------------------|---------------|
| Create API  Gateway at System Boundary | Controls all access using sign in authentication which then routes requests to internal services. This supports security.privacy (QA-3) ensuring a consistent point of entry for users of the system. |
| Add QueryAssistantService in the Business logic Layer | Handles student queries and AI processing which supports performance (QA-1) and overall scalability. |
| Add NotificationService in Business Logic Layer | Implements UC-2, which supports campus alerts  (UC-5). This ensures efficient notifications under heavy load, and supports scalability (QA-4) |
| Add DataSyncService in Integration Layer | Implementing this integrates UC-7, synching with LMS, registration as well as calendar systems. This also supports consistency and interoperability within the system (QA-7 & QA-5) |
| Create SystemOperationsModule in operations layer | This implements Uc-7 which handles monitoring the operations, health and zero-downtime updates of the system. |

---

## Step 6: Diagrams: 

- Context Diagram  
- Layer Diagram  
- Deployment Diagram  

---

## Step 7:

| **Scenario** | **Status** | **Design Decision Made** |
|-------------|------------|--------------------------|
| UC-1 Query Assistant | Completely Addressed | QueryAssistantService was added in the business logic layer to handle student AI queries and fast responses. |
| UC-2 Notifications | Completely Addressed | NotificationService was added to manage reminders and push notifications at smaller or larger scales. |
| UC-6 System Operations | Completely Addressed | SystemOperationsModules support system supervision tasks like runtime diagnostics, service health, deployment and any maintenance or updates that are required. |
| UC-7 Data Sync Services | Completely Addressed | Added DataSyncService to ensure information remains constituent across each subsystem and runs properly throughout the entire platform. |
| QA-1 Performance | Partially Addressed | Supports fast responses by distributing high-traffic features  into dedicated services and applying initial caching, improving responsiveness. |
| QA-7 Consistency | Completely Addressed | Supports cross system communication by adding the DataSyncsService and ExternalSystemConnectors which manage interactions with subsystems of the platform. This ensures consistent data flow, and simplifies evolving university systems. |

---

# Iteration 2

## Step 2: Iteration Goal

**Main Functionality:**

- UC-1: Query Assistant  
- UC-2 Notifications  
- UC-3: Schedule Manager  
- UC-7 Data Sync Services  

---

## Step 3: Elements to Refine from Iteration 1

- User Interaction Layer (presentation layer modules)  
- Business Logic Services (application/service modules)  
- Data Sync & Integration Layer (integration/data interface layers)  
- System Operations Layer (operation  modules)  

---

## Step 4: Design Concepts

| **Design Decision** | **Rationale** |
|---------------------|---------------|
| Adopting a Layered Architecture across UI, Business Logic, Integration and Operation layers | Layered system structure provides a clear separation of concerns, which simplifies responsibilities. This supports modifiability, making sure that each major area can work independently. A monolithic design would result in an increase in coupling which would cause dependencies. |
| Service Based Decomposition within Business Logic | Decomposing core functionality into service modules will support AIDAPS  use cases, while maintaining independence among important functional elements. |
| External System Connectors in Integration Layer | Specialized connectors like the LMSConnector isolate system dependencies allowing for architecture to adapt to changes in external university systems. Without this there would be an increase in coupling and a decrease in modificability. |
| Centralized System within Operations Layer | Monitoring, health checking, deployments and update management should be uniformly handled across all subsystems. A fragmented approach would result in inconsistent operational behaviour which is harder to control. |

---

## Step 5: Instantiate Architectural Elements

| **Design Decision & Location** | **Rationale** |
|--------------------------------|---------------|
| Make initial domain model for AIDAP | Setting a domain model early on helps identify the core concepts that are implemented across the key use cases that represent the main functionality. An initial model is created at this stage so that it can evolve in later iterations. |
| Map the use cases to domain objects | Domain objects and key use cases are associated together to ensure that the essential responsibilities that make the system functional are represented. This prevents missing out on important behaviour. |
| Splitting of domain objects across major architectural layers | The separation of domain objects across the UI, business logic, integration and operations layers provides clarity on which layer holds what responsibility. This establishes a structured approach to complex interfaces, preventing dependency. |
| Identify layer specific modules with clear interfaces | The modules group the systems main responsibilities like handling queries, notifications, data syncing and system operations. Clear interfaces support independence of the system for future updates. |
| Introduce connector abstractions for external systems | Abstracting LMS, and other subsystems into connector components isolates AIDAP from external API modifications. This lowers integration risk, maintaining stability should external systems evolve. |
| Establish operational modules for runtime support | Defining the systems operation modules ensure the system operates smoothly and deployment activities are coordinated across all layers. This helps in prevention of fragmented operational logic. |

---

## Step 6: 

- Domain Model Diagram  
- Sequence Diagram (Query Assistant)  

---

## Step 7:

| **Scenario** | **Status** | **Design Decision Made** |
|-------------|------------|--------------------------|
| UC-1 Query Assistant | Completely Addressed | QueryAssistantService was added in the business logic layer to handle student AI queries and fast responses. |
| UC-2 Notifications | Completely Addressed | NotificationService was added to manage reminders and push notifications at smaller or larger scales. |
| UC-3 Schedule Manager | Completely Addressed | SystemOperationsModules support system supervision tasks like runtime diagnostics, service health, deployment and any maintenance or updates that are required. |
| UC-7 Data Sync Services | Completely Addressed | Added DataSyncService to ensure information remains constituent across each subsystem and runs properly throughout the entire platform. |
| QA-1 Performance | Partially Addressed | Supports fast responses by distributing high-traffic features  into dedicated services and applying initial caching, improving responsiveness. |
| QA-7 Consistency | Completely Addressed | Supports cross system communication by adding the DataSyncsService and ExternalSystemConnectors which manage interactions with subsystems of the platform. This ensures consistent data flow, and simplifies evolving university systems. |
