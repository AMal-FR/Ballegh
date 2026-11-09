# User Stories

Format: **As a** (role) **I want** (goal) **so that** (benefit)

## Epic 1: Report Creation
| ID | Story | Acceptance Criteria | FR |
|---|---|---|---|
| US-01 | As a citizen, I want to report a problem with a photo so that it reaches the responsible agency. | I can choose the problem type and upload a photo; the location is captured automatically; a confirmation of receipt is shown. | FR-02, 03 |
| US-02 | As a citizen, I want the report to be routed automatically to the right agency so that I don't need to know who is responsible. | The report appears at the appropriate agency for its type with no manual step. | FR-04 |

## Epic 2: Status Tracking
| ID | Story | Acceptance Criteria | FR |
|---|---|---|---|
| US-03 | As a citizen, I want to track my report's status so that I know what happened. | The current status and the change history are shown. | FR-05, 07 |
| US-04 | As a citizen, I want a notification on every status change so that I don't have to keep opening the app. | A push notification arrives on every status change. | FR-08 |
| US-05 | As an official, I want to update a report's status so that the citizen can follow its progress. | The status change is logged with the time and my name. | FR-05, 07 |
| US-06 | As an official, I want to reject a false or out-of-scope report with a reason so that the list stays clean. | Rejection requires a reason and the citizen is notified. | FR-06 |

## Epic 3: Emergency (SOS)
| ID | Story | Acceptance Criteria | FR |
|---|---|---|---|
| US-07 | As a citizen, I want an emergency button that works with one tap so that I can report a fire or accident quickly. | One tap + confirmation sends the location immediately; the photo is optional and added after sending. | FR-09 |
| US-08 | As a citizen in an emergency, I want the report to go directly to civil defense/ambulance so that they respond faster. | It skips priority calculation and receives the highest priority. | FR-10 |
| US-09 | As a citizen with no internet, I want to send my location by SMS so that I can call for help. | The app suggests SMS when it detects there is no connection. | FR-11 |

## Epic 4: Offline Mode
| ID | Story | Acceptance Criteria | FR |
|---|---|---|---|
| US-10 | As a citizen, I want to report without internet so that the problem is not delayed. | The report is saved locally and shows "Pending Send". | FR-12, 15 |
| US-11 | As a citizen, I want the report to be sent automatically when the connection returns so that I don't need to resubmit. | Automatic sync with no duplicates; the report time is the creation time. | FR-13, 14 |

## Epic 5: Duplicate Merging
| ID | Story | Acceptance Criteria | FR |
|---|---|---|---|
| US-12 | As an official, I want duplicate reports to be merged so that I'm not flooded with similar reports. | A nearby report of the same category and time window is merged under a Master report. | FR-16, 17 |
| US-13 | As a citizen, I want to join an existing report so that I can follow it instead of duplicating it. | "Would you like to join an existing report?" is shown, and after joining I receive updates. | FR-17, 18 |

## Epic 6: Priority
| ID | Story | Acceptance Criteria | FR |
|---|---|---|---|
| US-14 | As an official, I want reports ordered by priority so that I start with the most severe. | The list is sorted and each report has a classification (Critical/High/Medium/Low). | FR-19 |
| US-15 | As an official, I want to adjust the formula weights so that I can tune the system to reality. | Changes apply to new calculations and are logged. | FR-21 |

## Epic 7: Rating and Trust
| ID | Story | Acceptance Criteria | FR |
|---|---|---|---|
| US-16 | As a citizen, I want to rate the solution and confirm it was solved. | A notification with (yes/no) + 1–5 stars + optional comment. | FR-22 |
| US-17 | As a citizen who answered "still not solved", I want the report reopened and escalated so that the problem isn't neglected. | The report is reopened and sent to the Official. | FR-23 |
| US-18 | As the system, I want to close a report automatically if no one responds within 72 hours. | Closure happens after the window. | FR-24 |
| US-19 | As the system, I want to update the reporter's trust based on the report's outcome so that honest reporters are rewarded and false ones reduced. | The score changes per the table, and SOS is not affected. | FR-25, 27 |
| US-20 | As an official, I want to limit reports from low-trust users. | A numeric limit or temporary block applies below the threshold. | FR-26 |

## Epic 8: Management and Monitoring
| ID | Story | Acceptance Criteria | FR |
|---|---|---|---|
| US-21 | As an official, I want a performance dashboard so that I can track delays and satisfaction. | Shows resolution time, average satisfaction, and reopen rate. | FR-28 |
| US-22 | As an official, I want to manage agencies, categories, and users. | Full CRUD on all three. | FR-29 |
