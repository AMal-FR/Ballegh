# Requirements

## 1. Business Requirements
| ID | Requirement |
|---|---|
| BR-01 | Make it easy for citizen reports to reach the correct agency without the citizen knowing which agency is responsible. |
| BR-02 | Reduce the duplicate reports that flood agencies. |
| BR-03 | Order reports by priority instead of arrival order. |
| BR-04 | Reduce false reports and measure reporter credibility. |
| BR-05 | Improve response time for emergencies. |
| BR-06 | Measure citizen satisfaction and whether the problem was truly solved. |
| BR-07 | Provide performance dashboards for agencies. |
| BR-08 | Give citizens transparency: they can see their report's status at any time. |

## 2. User Requirements
### Citizen
- UR-01: I can report a problem with a photo and an automatic location in a few steps.
- UR-02: I can report an emergency with one tap.
- UR-03: I can report even when there is no internet connection.
- UR-04: I can track my report's status and receive notifications.
- UR-05: I can join an existing report instead of duplicating it.
- UR-06: I can rate the solution and confirm that the problem was actually solved.

### Official
- UR-07: I can see the reports routed to my agency, ordered by priority.
- UR-08: I can update a report's status and add notes.
- UR-09: I can reject a false or out-of-scope report with a written reason.
- UR-10: I can monitor performance (resolution time, delays, reopen rate, average satisfaction).
- UR-11: I receive an escalation when a report is reopened.
- UR-12: I can manage agencies, categories, and users.
- UR-13: I can adjust the priority formula weights and the duplicate-merge thresholds.

## 3. System Requirements
### 3.1 Functional Requirements
| ID | Requirement | Priority |
|---|---|---|
| FR-01 | Registration, login, and account management for all roles (role-based access). | High |
| FR-02 | Create a report with a problem type, a photo, and an optional description. | High |
| FR-03 | Automatically capture the GPS location when a report is created. | High |
| FR-04 | Automatically route the report to the responsible agency based on its type. | High |
| FR-05 | Status tracking: Received → Under Review → Routed to Agency → In Progress → Resolved → Closed. | High |
| FR-06 | Side statuses: Merged, Rejected, Reopened. | High |
| FR-07 | Record every status change in `Status_History` with the time and the person responsible. | High |
| FR-08 | Send a push notification on every status change to all linked reporters. | High |
| FR-09 | SOS button for critical cases (fire, accident, gas leak) with one tap and a confirmation. | High |
| FR-10 | An SOS report gets the highest priority, skips normal priority calculation, and goes directly to civil defense/ambulance. | High |
| FR-11 | Suggest sending the location by SMS for SOS when there is no internet. | Medium |
| FR-12 | Store the report locally (SQLite/Hive) in a waiting queue when offline. | Medium |
| FR-13 | Record the report's time and location at creation time, not at send time. | Medium |
| FR-14 | Automatic background sync with a unique key per report to prevent double submission (idempotency key). | Medium |
| FR-15 | Show the citizen a clear "Pending Send" state. | Medium |
| FR-16 | Duplicate check: same category + distance + time window + original report not closed (+ optional image similarity). | Medium |
| FR-17 | Merge a duplicate under a Master Report, or ask "Would you like to join an existing report?". | Medium |
| FR-18 | A reporter who joins a report can track its status and receive notifications. | Medium |
| FR-19 | Calculate the priority score using the formula and classify it (Critical/High/Medium/Low). | Medium |
| FR-20 | Recalculate priority on every merge and as time passes. | Medium |
| FR-21 | Manage formula weights and merge thresholds from the Official's dashboard. | Medium |
| FR-22 | Send a rating notification when a report is Resolved: was it solved (yes/no) + 1–5 stars + optional comment. | Low |
| FR-23 | If the answer is "no": reopen the report and automatically escalate it to the Official. | Low |
| FR-24 | Automatically close the report if there is no response within 72 hours. | Low |
| FR-25 | Calculate and update the user trust score (starting at 50/100) according to the events table. | Low |
| FR-26 | Lower the priority of or hold back reports from low-trust users, and limit their report count or temporarily block them. | Low |
| FR-27 | Exempt SOS reports from the effect of a low trust score. | Low |
| FR-28 | Agency dashboard (average satisfaction, reopen rate, resolution time, delays). | Low |
| FR-29 | Manage agencies, categories, and users (CRUD) for the Official. | Medium |

### 3.2 Non-Functional Requirements
| ID | Category | Requirement |
|---|---|---|
| NFR-01 | Performance | Receive and route an SOS report in under 3 seconds (when connected). |
| NFR-02 | Availability | At least 99.5% uptime. |
| NFR-03 | Reliability | No report stored locally may be lost before sync. |
| NFR-04 | Security | Encrypted communication (HTTPS/TLS) and hashed password storage. |
| NFR-05 | Privacy | Citizen and location data are shared only with the relevant agency. |
| NFR-06 | Usability | Simple interface; creating a report takes at most 4 steps. |
| NFR-07 | Scalability | Handle sudden spikes in reports (disasters/large events). |
| NFR-08 | Compatibility | Runs on Android and iOS. |
| NFR-09 | Auditability | Every status change and settings change is logged and traceable. |
| NFR-10 | Maintainability | Weights and thresholds are adjustable without code changes. |

## 4. Domain Requirements (Business Rules)
| ID | Rule |
|---|---|
| DR-01 | Every problem category is linked to at least one responsible agency (water, electricity, sanitation, civil defense, ambulance, etc.). |
| DR-02 | Duplicate conditions: same category (mandatory); distance under 50 m (100 m for water and garbage); time window: fire/accident 2 hours, other problems 24 hours to 7 days; original report not closed. |
| DR-03 | Priority formula = Severity×0.40 + Reporter Count×0.20 + Location Sensitivity×0.15 + Reporter Trust×0.15 + Waiting Time×0.10 (each component scaled 0–100). |
| DR-04 | Classification: Critical ≥ 80, High 60–79, Medium 40–59, Low < 40. |
| DR-05 | Trust score: starts at 50; confirmed valid report +5; resolved and confirmed by citizen +3; classified false/misleading −15; intentional duplicate/abusive −5. |
| DR-06 | SOS: highest priority, goes to civil defense/ambulance, and is not affected by the reporter's trust score. |
| DR-07 | A merged report increases the Master report's reporter count and priority. |
| DR-08 | A report is not finally "resolved" until the citizen confirms or the 72-hour window expires. |
| DR-09 | A reopened report is escalated to the Official. |
| DR-10 | Location sensitivity increases near a hospital, a school, or a crowded area. |
