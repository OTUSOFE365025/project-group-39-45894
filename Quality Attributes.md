| **ID** | **Quality Attribute** | **Description** | **Associated Use Cases (ID)** |
|:-------|:----------------------|:----------------|:------------------------------|
| QA-1 | Performance | Multiple students send queries (When is my next exam/assignment?) during peak loads. No queries fail and 90–95% of responses are returned within 2 seconds. | UC-1, UC-2, UC-3, UC-6, UC-7 |
| QA-2 | Availability | The system automatically falls to a backup point and resumes all services normally when a failure occurs in the AIDAP system during normal operations. | UC-1, UC-2, UC-4, UC-5, UC-6 |
| QA-3 | Security/Privacy | A student logs into the system through the university SSO to request their grades; only authenticated student data are displayed. Additionally, all accesses are logged. | UC-1, UC-3, UC-4, UC-5, UC-6 |
| QA-4 | Scalability | During peak times (such as course registration) 5000 concurrent users interact with the assistant; the system scales to maintain efficient response times without exceeding its resource limits. | UC-1, UC-2, UC-5, UC-6, UC-7 |
| QA-5 | Interoperability | The AIDAP system interacts and analyzes institutional integrations (LMS, registration, calendars) using REST APIs. If one of the systems is unavailable (failure/maintenance), the system retries automatically. | UC-1, UC-2, UC-3, UC-4, UC-7 |
| QA-6 | Modifiability | New external systems, data sources, and AI services are integrated without changing existing components. | UC-6, UC-7, UC-4 |
| QA-7 | Consistency | An instructor updates an assignment due date in the LMS; the change is reflected on the student’s dashboard within 5 minutes. | UC-2, UC-3, UC-4, UC-7 |
