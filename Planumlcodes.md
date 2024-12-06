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
