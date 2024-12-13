# User Requirements Document (URD)

## 1. Introduction

### 1.1 Purpose
This document outlines the user requirements for a **Google Docs clone application**. It aims to guide the design, development, and testing of the application to ensure it meets the needs of its users, including document creators, collaborators, and administrators.

### 1.2 Scope
The Google Docs clone will be a **web-based document editing application** that supports real-time collaboration, document management, and basic text formatting. Users will be able to create, edit, and share documents.

### 1.3 Definitions, Acronyms, and Abbreviations
- **User**: An individual who uses the application to create and edit documents.
- **Admin**: The entity responsible for managing the app’s operations.
- **RT**: Real-time.

### 1.4 References
- `Stakeholders.md`
- `Project.md`

## 2. User Characteristics

### 2.1 Users
- Typically web or smartphone users familiar with basic app navigation.
- Expect a seamless and fast document creation and editing experience.
- Value real-time collaboration, version control, and document sharing.

### 2.2 Admins
- Manage Google Docs users, documents, and application operations.
- As an Admin I must be able to monitor and control over document activities and docs user accounts.

## 3. Functional Requirements

### 3.1 User Registration and Login
As a Google Doc User 
- I must be able to register using an email address.
- I must be able to log in with their credentials.
- If I forget my password, I should have an option to reset it .

### 3.2 Document Creation and Management
- I must be able to create, edit, and delete documents.
- I must be able to organize documents into folders.
- I must be able to view and manage their documents, including document sharing and access permissions.

### 3.3 Real-Time Collaboration
- I must be able to collaborate on documents with multiple users simultaneously.
- If I make any changes it must be reflected in real-time to my  collegues/friends.
- I should be able to use version control to see past versions and revert changes.

### 3.4 Document Formatting
- I must have access to basic text formatting features, such as bold, italic, underline, and lists.
- I must be able to apply headings, paragraph styles, and font options.
- I should be able to download documents in different formats (e.g., PDF, DOCX).

### 3.5 Comments and Feedback
- I must be able to comment on specific parts of the document for feedback.
- I must be able to reply to comments and mark them as resolved.
-  Whenever I make a new commit Notifications should be sent .

### 3.6 File Sharing
- I must be able to share documents with others via a shareable link.
- I must be able to set permissions for shared documents (view, comment, edit).

### 3.7 Notifications
- I must receive notifications for document sharing, comments, and updates.
- As an Admin I should receive notifications for important system events.

### 3.8 Admin Panel
If I were an admin:
- I must be able to manage user accounts (approve, suspend, or delete users).
- I must be able to view real-time data on document activity.
- I must have access to document history and activity logs.

## 4. Non-Functional Requirements

### 4.1 Performance
- I expect the application to load within 2 seconds under normal network conditions.
- I expect Real-time collaboration and updates must be near-instant for all users.

### 4.2 Security
- My data must be encrypted both in transit and at rest.
- The application must comply with data protection regulations (e.g., GDPR).
- For me  there should be Secure user authentication methods, such as multi-factor authentication, must be available.

### 4.3 Usability
- Whenever I use the User interface it must be intuitive and easy to navigate .
-The UI must be responsive when I use it on different devices and screen sizes.

### 4.4 Reliability
- The application must be available 99.9% of the time, with minimal downtime.
- Backup systems should prevent No data loss in the event of a failure.

### 4.5 Scalability
- The system must scale to support a growing number of docs users and documents without performance degradation.
- The backend should support new features and upgrades without significant rework.

## 5. Assumptions and Dependencies
-  third-party services will handle cloud storage, notifications, and payment processing (if applicable).
- I assume that I will have access to stable internet connections and modern web browsers.

## 6. Acceptance Criteria
- The application must pass all functional and non-functional tests.
- Feedback during beta testing must be resolved before release.
- The application must meet outlined security and performance test.

## 7. Conclusion
This document defines the docs user requirements for the Google Docs clone application. It serves as a guideline for the development team to ensure the final product meets the needs of the users and achieves the project’s objectives.
