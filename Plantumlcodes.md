# System Context Diagram

```plantuml
@startuml
actor User
actor Admin
package "External Systems" {
  [Google Drive API]
  [Firebase Auth]
}
package "Google Docs System" {
  [Frontend]
  [Backend Services]
  [Database]
}

User --> [Frontend]
Admin --> [Frontend]
[Frontend] --> [Backend Services]
[Backend Services] --> [Database]
[Backend Services] --> [Google Drive API]
[Backend Services] --> [Firebase Auth]
@enduml

```

# Container Diagram

```plantuml
@startuml
!define RECTANGLE class

package "Frontend Components" {
  RECTANGLE WebClient {
    +displayDocumentsList(): void
    +renderDocumentEditor(documentId: String): void
    +handleRealTimeCollaboration(documentId: String): void
    +manageUserAuthentication(): Boolean
    +integrateNotifications(): void
    +uploadFilesToCloud(): void
  }

  RECTANGLE MobileClient {
    +displayDocumentsList(): void
    +renderDocumentEditor(documentId: String): void
    +handleRealTimeCollaboration(documentId: String): void
    +manageUserAuthentication(): Boolean
    +integrateNotifications(): void
    +uploadFilesToCloud(): void
    +optimizeForOfflineMode(): void
  }

  RECTANGLE SharedComponents {
    +HeaderNavBar: ReusableComponent
    +FooterNavBar: ReusableComponent
    +SideMenu: ReusableComponent
    +DocumentCard: ReusableComponent
    +NotificationWidget: ReusableComponent
  }

  RECTANGLE RealTimeCollaborationModule {
    +connectToWebSocket(documentId: String): Boolean
    +syncCollaborativeEdits(): void
    +resolveMergeConflicts(): Boolean
  }

  RECTANGLE AuthModule {
    +handleLogin(email: String, password: String): Boolean
    +handleLogout(): void
    +validateSession(): Boolean
  }

  RECTANGLE NotificationModule {
    +displayNotifications(): void
    +listenForUpdates(): void
  }
}

WebClient --> SharedComponents : "Uses reusable UI components"
MobileClient --> SharedComponents : "Uses reusable UI components"
WebClient --> RealTimeCollaborationModule : "Manages real-time collaboration"
MobileClient --> RealTimeCollaborationModule : "Manages real-time collaboration"
WebClient --> AuthModule : "Authenticates user"
MobileClient --> AuthModule : "Authenticates user"
WebClient --> NotificationModule : "Handles in-app notifications"
MobileClient --> NotificationModule : "Handles in-app notifications"
RealTimeCollaborationModule --> WebSocketServer : "Syncs changes in real-time"
AuthModule --> Backend.AuthService : "Authenticates with backend"
NotificationModule --> Backend.NotificationService : "Fetches notifications"
@enduml


```
### User
```plantuml
@startuml
actor "User" as User

package "User Side" {
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
}

' User interacts with the WebApp through UI for document-related tasks
User --> WebApp : Uses UI for document tasks

' WebApp sends API requests to BackendAPI
WebApp --> BackendAPI : Sends API requests

' BackendAPI interacts with different services
BackendAPI --> DocStorage : Accesses document data
BackendAPI --> AuthService : Verifies user identity
BackendAPI --> NotificationService : Sends notifications

' Document storage service interacts with cloud storage
DocStorage --> CloudStorage : Stores documents

' Authentication service integrates with third-party services
AuthService --> ThirdPartyAuth : OAuth/Firebase Auth Integration
@enduml

```
### Admin 
```plantuml
@startuml
actor Admin

package "Admin Panel" {
    package "User Management" {
        class ViewEditDeleteUsers
        class RoleAssignment
        class InviteUsers
    }

    package "System Monitoring" {
        class ViewServerHealth
        class LogsAPIActivity
        class RealTimeUsageTracking
    }

    package "Document Management" {
        class ViewFlagDeleteDocuments
        class ManageVersionHistory
    }

    package "External Services" {
        class ConfigureCloudStorage
        class ManageAuthServices
    }

    package "Reporting & Analytics" {
        class GenerateActivityReports
        class ExportReports
    }

    package "Platform Settings" {
        class BrandingLogoTheme
        class FeatureToggles
        class EmailConfigurations
    }
}

Admin --> ViewEditDeleteUsers : Manages Users
Admin --> RoleAssignment : Assigns Roles
Admin --> InviteUsers : Sends Invitations

Admin --> ViewServerHealth : Monitors Server Health
Admin --> LogsAPIActivity : Reviews Logs
Admin --> RealTimeUsageTracking : Tracks Usage

Admin --> ViewFlagDeleteDocuments : Reviews Documents
Admin --> ManageVersionHistory : Manages Versions

Admin --> ConfigureCloudStorage : Configures Storage
Admin --> ManageAuthServices : Manages Auth Services

Admin --> GenerateActivityReports : Generates Reports
Admin --> ExportReports : Exports Reports

Admin --> BrandingLogoTheme : Customizes Branding
Admin --> FeatureToggles : Manages Features
Admin --> EmailConfigurations : Updates Email Settings
@enduml
```
# Component Diagram

```plantuml
@startuml
actor "User" as EndUser
actor "Administrator" as PlatformAdmin
actor "DevOps Engineer" as DevOps

package "User Interfaces" {
    [Desktop Application] as DesktopApp
    [Mobile Application] as MobileApp
    [Web Dashboard] as WebDashboard
}

package "Backend Services" {
    [API Gateway] as APIGateway
    [Authentication Service] as AuthService
    [Data Management Service] as DataService
    [Notification Service] as NotifyService
    [Payment Processing] as PaymentService
}

package "Storage Systems" {
    [Database] as Database
    [Cloud Storage] as CloudStorage
    [Backup System] as BackupSystem
}

package "Third-Party Integrations" {
    [Third-Party Authentication] as ThirdPartyAuth
    [External Payment Gateway] as PaymentGateway
    [Analytics Service] as AnalyticsService
}

EndUser --> DesktopApp : Use Desktop
EndUser --> MobileApp : Use Mobile
EndUser --> WebDashboard : Use Web Dashboard
PlatformAdmin --> WebDashboard : Manage Platform
DevOps --> APIGateway : Deploy Changes

DesktopApp --> APIGateway : Request Data
MobileApp --> APIGateway : Request Sync
WebDashboard --> APIGateway : Send API Requests
APIGateway --> AuthService : Authenticate Requests
APIGateway --> DataService : Fetch/Store Data
APIGateway --> NotifyService : Send Notifications
APIGateway --> PaymentService : Process Payments

AuthService --> Database : Verify User Credentials
DataService --> Database : Store/Fetch Data
NotifyService --> EndUser : Push Alerts
PaymentService --> PaymentGateway : Validate Transactions

BackupSystem --> Database : Backup Data
DataService --> CloudStorage : Store Files
CloudStorage --> BackupSystem : Archive Backups
AnalyticsService --> APIGateway : Provide Metrics
ThirdPartyAuth --> AuthService : OAuth Authentication
@enduml
```
### Frontend Component
```plantuml
@startuml
title Google Docs System - C4 Level 2: Frontend Container

actor "User" as User #lightblue
actor "Admin" as Admin #lightblue

package "Frontend" {
  [Web App] <<container>> #lightgreen
}

package "Backend Services" {
  [Authentication Service] <<container>> #lightgreen
  [Document Management Service] <<container>> #lightgreen
  [Notification Service] <<container>> #lightgreen
}

User --> [Web App] : "Access via Browser"
Admin --> [Web App] : "Access Admin Dashboard"
[Web App] --> [Authentication Service] : "Login and User Authentication"
[Web App] --> [Document Management Service] : "Edit and Share Documents"
[Web App] --> [Notification Service] : "Fetch Notifications"

@enduml

```

### Backend Component
```plantuml
@startuml
title Google Docs System - C4 Level 2: Backend Services Container

actor "Frontend" as Frontend #lightblue
package "Backend Services" {
  [Authentication Service] <<container>> #lightgreen
  [Document Management Service] <<container>> #lightgreen
  [Notification Service] <<container>> #lightgreen
  [Analytics Service] <<container>> #lightgreen
}

package "Database" {
  [User Database] <<container>> #lightgrey
  [Document Database] <<container>> #lightgrey
}

Frontend --> [Authentication Service] : "Authenticate Users"
Frontend --> [Document Management Service] : "Handle Document CRUD"
Frontend --> [Notification Service] : "Retrieve Notifications"
[Authentication Service] --> [User Database] : "Verify User Credentials"
[Document Management Service] --> [Document Database] : "Store Document Data"
[Notification Service] --> [User Database] : "Fetch User Notification Preferences"

@enduml

```
### Database Component
```plantuml
@startuml
title Google Docs System - C4 Level 2: Database Container

package "Database" {
  [User Database] <<container>> #lightgrey
  [Document Database] <<container>> #lightgrey
  [Notifications Collection] <<container>> #lightgrey
}

package "Backend Services" {
  [Authentication Service] <<container>> #lightgreen
  [Document Management Service] <<container>> #lightgreen
  [Notification Service] <<container>> #lightgreen
}

[Authentication Service] --> [User Database] : "User Authentication Data"
[Document Management Service] --> [Document Database] : "Store and Retrieve Documents"
[Notification Service] --> [Notifications Collection] : "Store Notifications"
[Document Management Service] --> [User Database] : "Access User Metadata"

@enduml
```
### Container: External Systems

```plantuml
@startuml
!define RECTANGLE class

package "Frontend Components" {
  RECTANGLE WebClient {
    +displayDocumentsList(): void
    +renderDocumentEditor(documentId: String): void
    +handleRealTimeCollaboration(documentId: String): void
    +manageUserAuthentication(): Boolean
    +integrateNotifications(): void
    +uploadFilesToCloud(): void
  }

  RECTANGLE MobileClient {
    +displayDocumentsList(): void
    +renderDocumentEditor(documentId: String): void
    +handleRealTimeCollaboration(documentId: String): void
    +manageUserAuthentication(): Boolean
    +integrateNotifications(): void
    +uploadFilesToCloud(): void
    +optimizeForOfflineMode(): void
  }

  RECTANGLE SharedComponents {
    +HeaderNavBar: ReusableComponent
    +FooterNavBar: ReusableComponent
    +SideMenu: ReusableComponent
    +DocumentCard: ReusableComponent
    +NotificationWidget: ReusableComponent
  }

  RECTANGLE RealTimeCollaborationModule {
    +connectToWebSocket(documentId: String): Boolean
    +syncCollaborativeEdits(): void
    +resolveMergeConflicts(): Boolean
  }

  RECTANGLE AuthModule {
    +handleLogin(email: String, password: String): Boolean
    +handleLogout(): void
    +validateSession(): Boolean
  }

  RECTANGLE NotificationModule {
    +displayNotifications(): void
    +listenForUpdates(): void
  }
}

WebClient --> SharedComponents : "Uses reusable UI components"
MobileClient --> SharedComponents : "Uses reusable UI components"
WebClient --> RealTimeCollaborationModule : "Manages real-time collaboration"
MobileClient --> RealTimeCollaborationModule : "Manages real-time collaboration"
WebClient --> AuthModule : "Authenticates user"
MobileClient --> AuthModule : "Authenticates user"
WebClient --> NotificationModule : "Handles in-app notifications"
MobileClient --> NotificationModule : "Handles in-app notifications"
RealTimeCollaborationModule --> WebSocketServer : "Syncs changes in real-time"
AuthModule --> Backend.AuthService : "Authenticates with backend"
NotificationModule --> Backend.NotificationService : "Fetches notifications"
@enduml
```
