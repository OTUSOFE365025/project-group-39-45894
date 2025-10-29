| Use Case ID | Title                    | Description                                                                                                                                                                                              | Stakeholders           | Requirements                        |
|-------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|--------------------------------------|
| UC-1        | Query Assistant           | A student interacts with AIDAP through voice or text to ask questions (deadlines, course info, exam date). The system processes queries after authentication using AI, giving a secure real-time response. | Students                | R1, R3, R4, R5, R8                  |
| UC-2        | Notifications             | Students can see personalized notifications like upcoming events or deadlines. AIDAP retrieves cached data to give real-time responses.                                                                  | Students                | R2, R3, RS6, RS12, RS13             |
| UC-3        | Schedule Manager          | Students upload their deadlines and events to calendars, set preferred notifications, and manage their schedule. Data syncs securely.                                                                     | Students                | R2, R3, RS6, RS12, RS13             |
| UC-4        | Course Content Publisher  | Lecturers publish announcements and share course content. AIDAP ensures valid users are granted access securely.                                                                                          | Lecturers               | R3, R6, R8, RL2, RL3               |
| UC-5        | Alerts                    | Administrators can send out announcements that reach all users across campus, and monitor information going out under high load.                                                                          | Administrators          | RA1, RA2, RA3, RA5, R7             |
| UC-6        | System Operations         | Maintainers monitor the overall health of the system, deploy zero-downtime updates, configure certain services, and ensure stable performance.                                                             | System Maintainer       | RM1, RM2, RM3, RM5, R7             |
| UC-7        | Data Sync Services        | AIDAP synchronizes with existing systems through secure connections like LMS, course registration, and calendar service databases.                                                                        | Data Source Systems     | RD1, RD2, RD3, RD4, R3            |


Use Case Model:




<img width="645" height="533" alt="image" src="https://github.com/user-attachments/assets/04862186-afaa-4a16-a458-12ad2e5df253" />
