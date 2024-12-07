# System Context Diagram

```plantuml
@startuml
!define RECTANGLE class

actor User
actor Admin
actor Developer

package "Web Client" {
  RECTANGLE "Web Application (UI)" as WebApp {
    WebApp : User Interface
    WebApp : Document Creation
    WebApp : Real-Time Collaboration
    WebApp : File Sharing
    WebApp : Commenting and Suggestions
    WebApp : Version History
  }
}

package "Server Side" {
  RECTANGLE "Backend API" as BackendAPI {
    BackendAPI : Handles requests from WebApp
    BackendAPI : User Authentication
    BackendAPI : Document Management
    BackendAPI : Collaboration Sync
    BackendAPI : Commenting & Suggestion Handling
    BackendAPI : Version History Management
  }

  RECTANGLE "Document Storage Service" as DocStorage {
    DocStorage : Stores user documents
    DocStorage : Version History Storage
  }
```

# Container Diagram

![Container Diagram](#)

```plantuml
@startuml
actor User
actor Admin
actor Developer

node "Web Client" {
    node "Web Application (UI)" as WebApp
}

node "Server Side" {
    node "Backend API" as BackendAPI
    node "Document Storage Service" as DocStorage
    node "Authentication Service" as AuthService
    node "Notification Service" as NotificationService
}

node "External Services" {
    node "Cloud Storage" as CloudStorage
    node "Third-Party Authentication" as ThirdPartyAuth
}

User --> WebApp : Uses UI for document tasks
Admin --> WebApp : Manages platform
WebApp --> BackendAPI : Sends API requests
BackendAPI --> DocStorage : Accesses document data
BackendAPI --> AuthService : Verifies user identity
BackendAPI --> NotificationService : Sends notifications
DocStorage --> CloudStorage : Stores documents
AuthService --> ThirdPartyAuth : OAuth/Firebase Auth Integration

@enduml
