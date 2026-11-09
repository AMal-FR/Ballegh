# Diagrams

## 1. Use Case Diagram
(PlantUML: paste the code into https://www.plantuml.com/plantuml or use a PlantUML extension in VS Code)

```plantuml
@startuml
left to right direction
actor "Citizen" as C
actor "Official" as O
actor "Notification / SMS Service" as N <<system>>

rectangle "Balagh System" {
  usecase "Log In" as UC1
  usecase "Create Report" as UC2
  usecase "Send SOS Report" as UC3
  usecase "Save Report Offline" as UC4
  usecase "Track Report Status" as UC5
  usecase "Join Existing Report" as UC6
  usecase "Rate Solution" as UC7
  usecase "Check Duplicates and Merge" as UC8
  usecase "Calculate Priority" as UC9
  usecase "Update Report Status" as UC10
  usecase "Reject Report" as UC11
  usecase "View Performance Dashboard" as UC12
  usecase "Manage Agencies and Categories" as UC13
  usecase "Manage Users" as UC14
  usecase "Configure Priority Weights" as UC15
  usecase "Update User Trust Score" as UC16
  usecase "Send Notification" as UC17
}

C --> UC1
C --> UC2
C --> UC3
C --> UC5
C --> UC6
C --> UC7
O --> UC1
O --> UC10
O --> UC11
O --> UC12
O --> UC13
O --> UC14
O --> UC15

UC2 ..> UC4 : <<extend>> (no internet)
UC2 ..> UC8 : <<include>>
UC2 ..> UC9 : <<include>>
UC3 ..> UC4 : <<extend>>
UC6 ..> UC8 : <<include>>
UC10 ..> UC17 : <<include>>
UC7 ..> UC16 : <<include>>
UC17 --> N
@enduml
```

## 2. Class Diagram
(Mermaid: renders directly on GitHub)

```mermaid
classDiagram
class User {
  +int id
  +String name
  +String phone
  +String email
  +String passwordHash
  +Role role
  +int trustScore
  +bool isBlocked
  +login()
  +updateTrustScore(delta)
}
class Citizen
class Official {
  +updateStatus(report, status)
  +rejectReport(report, reason)
  +viewDashboard()
  +manageAgencies()
  +manageUsers()
  +setPriorityWeights()
}
class Agency {
  +int id
  +String name
}
class Category {
  +int id
  +String name
  +int severity
  +int duplicateRadiusM
  +int duplicateWindowHours
  +bool isEmergency
}
class Report {
  +UUID uniqueKey
  +String description
  +double latitude
  +double longitude
  +DateTime createdAt
  +Status status
  +float priorityScore
  +PriorityLevel level
  +bool isSOS
  +Report masterReport
  +calculatePriority()
  +merge(master)
  +reopen()
}
class Media {
  +int id
  +String url
}
class StatusHistory {
  +int id
  +Status oldStatus
  +Status newStatus
  +DateTime changedAt
}
class Rating {
  +int stars
  +bool isResolved
  +String comment
}
class Notification {
  +int id
  +String message
  +DateTime sentAt
  +bool isRead
}
class PriorityConfig {
  +float severityW
  +float reportersW
  +float locationW
  +float trustW
  +float waitW
}
class OfflineQueue {
  +List~Report~ pending
  +sync()
}

User <|-- Citizen
User <|-- Official
Agency "1" o-- "*" Official
Agency "1" -- "*" Category : responsible for
Category "1" -- "*" Report
Citizen "1" -- "*" Report : submits
Report "1" -- "*" Media
Report "1" -- "*" StatusHistory
Report "1" -- "0..*" Report : merged under
Report "1" -- "0..1" Rating
Citizen "1" -- "*" Rating
User "1" -- "*" Notification
Report "*" -- "1" Agency : routed to
Citizen "1" -- "1" OfflineQueue
PriorityConfig <.. Report : used by
```

**Note:** These diagrams are a first draft. Review and refine them as your analysis progresses.
