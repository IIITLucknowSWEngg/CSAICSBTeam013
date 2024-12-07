# Cross-Reference Matrix

The Cross-Reference Matrix maps the relationships between the different features, actors, and system components of the project.

| *Feature/Functionality*        | *User* | *Admin* | *WebApp (UI)* | *Backend API*      | *Document Storage Service* | *Authentication Service* | *Notification Service* | *Cloud Storage* | *Third-Party Auth* |
|----------------------------------|----------|-----------|------------------|-----------------------|------------------------------|----------------------------|---------------------------|-------------------|-----------------------|
| User Interface (UI)              | ✅        | ✅         | ✅                |                       |                              |                            |                           |                   |                       |
| Document Creation                | ✅        |           | ✅                | ✅                     | ✅                            |                            |                           |                   |                       |
| Real-Time Collaboration          | ✅        |           | ✅                | ✅                     | ✅                            |                            |                           |                   |                       |
| File Sharing                     | ✅        |           | ✅                | ✅                     | ✅                            |                            |                           |                   |                       |
| Commenting and Suggestions       | ✅        | ✅         | ✅                | ✅                     |                              |                            | ✅                         |                   |                       |
| Version History                  | ✅        | ✅         | ✅                | ✅                     | ✅                            |                            |                           |                   |                       |
| User Authentication              | ✅        | ✅         | ✅                | ✅                     |                              | ✅                          |                           |                   | ✅                     |
| Multi-Factor Authentication      | ✅        | ✅         |                  |                       |                              | ✅                          |                           |                   | ✅                     |
| Document Management              | ✅        | ✅         | ✅                | ✅                     | ✅                            |                            |                           |                   |                       |
| Sends Notifications              | ✅        | ✅         |                  | ✅                     |                              |                            | ✅                         |                   |                       |
| OAuth Login                      | ✅        | ✅         |                  |                       |                              | ✅                          |                           |                   | ✅                     |
| Stores Documents                 | ✅        | ✅         |                  | ✅                     | ✅                            |                            |                           | ✅                 |                       |
| Manages Platform                 |          | ✅         | ✅                | ✅                     | ✅                            | ✅                          | ✅                         |                   | ✅                     |

---

## Explanation of the Columns
- *Features/Functionalities*: Describes the functionalities or processes involved in the system.
- *Actors: Includes **User* and *Admin*—the main people interacting with the system.
- *System Components*:
  - *WebApp (UI)*: The user-facing interface for performing operations.
  - *Backend API*: Handles logic, requests, and data processing.
  - *Document Storage Service*: Stores and manages documents and their version histories.
  - *Authentication Service*: Handles login, multi-factor authentication, and identity management.
  - *Notification Service*: Sends notifications related to comments, changes, etc.
  - *External Services*:
    - *Cloud Storage*: Stores documents externally (e.g., AWS S3).
    - *Third-Party Auth*: Integrates with external authentication providers like OAuth/Firebase.

---

## Benefits of the Cross-Reference Matrix
- *Traceability*: Ensures all features have proper mappings to system components and actors.
- *Gap Analysis*: Identifies any missing functionality or unconnected components.
- *Validation*: Helps verify if each requirement is being fulfilled by the system.
