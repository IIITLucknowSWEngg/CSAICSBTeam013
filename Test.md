# Test Plan

## 1. Introduction

This document outlines the test strategy, objectives, scope, and test cases for the project. The goal is to ensure that all system components function as expected and meet the defined requirements.

---

## 2. Testing Scope

### Features to Test
- *User Functionality:*
  - Document creation, editing, sharing, and collaboration.
  - Login and registration.
  - Real-time collaboration.
- *Admin Functionality:*
  - User management.
  - System monitoring.
  - Report generation.
  - Platform configuration.
- *External Integrations:*
  - AWS S3 for document storage.
  - Firebase Auth for third-party authentication.
- *Non-functional Requirements:*
  - Performance and scalability.
  - Security measures, including role-based access.

---

# 3. Test Scenarios for Google Docs Clone

---

## Feature: User Registration

| Test ID       | TC-REG-001                                                |
|--------------------|---------------------------------------------------------------|
| Description    | Verify that a user can successfully register with valid information. |
| Precondition   | User is on the registration page.                             |
| Steps          | 1. The user enters valid information (name, email, password). <br> 2. The user submits the registration form. <br> 3. The user checks their email inbox, opens the confirmation email, and clicks the confirmation link to activate their account. |
| Expected Result| 1. The user should see a success message indicating "Registration Successful." <br> 2. The user should be redirected to the login page, displaying fields for entering login credentials. <br> 3. A database entry is created with user details, default status, and timestamp, updating to "active" after email confirmation. |
| Status         | Pending/Pass/Fail  |

### Chai.js Code

```javascript
describe('User Registration', function() {
  it('should register user successfully', function() {
    registrationPage.open();
    registrationPage.fillRegistrationForm('Jane Doe', 'jane@example.com', 'securePassword');
    registrationPage.submitForm();
    expect(registrationPage.getSuccessMessage()).to.equal('Registration successful');
    expect(browser.getUrl()).to.include('/login');
  });
});
```

## Feature: User Login

| *Test ID*       | *TC-LOG-001*                                               |
|--------------------|--------------------------------------------------------------|
| *Description*    | Verify that a user can successfully log in with valid credentials. |
| *Precondition*   | User is on the login page.                                   |
| *Steps*          | 1. The user enters valid credentials (email, password). <br> 2. The user submits the login form. |
| *Expected Result*| The user should be successfully logged in and redirected to the dashboard. |
| *Status*         | Pending/Pass/Fail                                            |

### Chai.js Code

```javascript
describe('User Login', function() {
  it('should login user successfully', function() {
    loginPage.open();
    loginPage.enterCredentials('jane@example.com', 'securePassword');
    loginPage.submitLogin();
    expect(loginPage.getWelcomeMessage()).to.include('Welcome, Jane Doe');
    expect(browser.getUrl()).to.include('/dashboard');
  });
});

```
## Feature: Admin Registration

| *Test ID*       | *TC-ADM-REG-001*                                          |
|--------------------|-------------------------------------------------------------|
| *Description*    | Verify that an admin can successfully register with valid information. |
| *Precondition*   | Admin is on the registration page.                          |
| *Steps*          | 1. The admin enters valid information (name, email, password). <br> 2. The admin submits the registration form. |
| *Expected Result*| 1. The admin should be successfully registered and redirected to the admin login page. <br> 2. A database entry is created with admin details, hashed password, and role set to "admin," along with a registration timestamp.|
| *Status*         | Pending/Pass/Fail                                           |

### Chai.js Code

```javascript
describe('Admin Registration', function() {
  it('should register admin successfully', function() {
    adminRegistrationPage.open();
    adminRegistrationPage.fillRegistrationForm('Admin User', 'admin@example.com', 'adminPassword');
    adminRegistrationPage.submitForm();
    expect(adminRegistrationPage.getSuccessMessage()).to.equal('Registration successful');
    expect(browser.getUrl()).to.include('/admin-login');
  });
});
```
## Feature: Admin Login

| *Test ID*       | *TC-ADM-LOG-001*                                          |
|--------------------|-------------------------------------------------------------|
| *Description*    | Verify that an admin can successfully log in with valid credentials. |
| *Precondition*   | Admin is on the admin login page.                           |
| *Steps*          | 1. The admin enters valid credentials (email, password). <br> 2. The admin submits the login form. |
| *Expected Result*| 1. The admin should be successfully logged in and redirected to the admin dashboard. <br> 2. A session entry is created in the database with the admin ID, login timestamp, and session token. |
| *Status*         | Pending/Pass/Fail                                           |

### Chai.js Code

```javascript
describe('Admin Login', function() {
  it('should login admin successfully', function() {
    adminLoginPage.open();
    adminLoginPage.enterCredentials('admin@example.com', 'adminPassword');
    adminLoginPage.submitLogin();
    expect(adminLoginPage.getWelcomeMessage()).to.include('Welcome, Admin User');
    expect(browser.getUrl()).to.include('/admin-dashboard');
  });
});
```
## Feature: Document Creation

| *Test ID*       | *TC-DOC-001*                                              |
|--------------------|-------------------------------------------------------------|
| *Description*    | Verify that a user can successfully create a new document.  |
| *Precondition*   | User is logged in and on the document creation page.        |
| *Steps*          | 1. The user clicks on the "Create New Document" button. <br> 2. The user enters content into the new document. <br> 3. The user saves the document. |
| *Expected Result*| 1. The user should see a success message indicating "Document Created Successfully." <br> 2. The document should appear in the user's document list. <br> 3. A database entry is created with the document's title, content, creator's user ID, and timestamp. |
| *Status*         | Pending/Pass/Fail                                           |

### Chai.js Code

```javascript
describe('Document Creation', function() {
  it('should create a new document successfully', function() {
    documentPage.open();
    documentPage.clickCreateNew();
    documentPage.enterContent('This is a new document.');
    documentPage.saveDocument();
    expect(documentPage.getSuccessMessage()).to.equal('Document created and saved successfully');
    expect(browser.getUrl()).to.include('/document');
  });
});
```
## Feature: Real-Time Collaboration

| *Test ID*       | *TC-RTC-001*                                                |
|--------------------|---------------------------------------------------------------|
| *Description*    | Verify that multiple users can collaborate on the same document in real-time. |
| *Precondition*   | The document is shared with another user.                     |
| *Steps*          | 1. User A opens the document. <br> 2. User B opens the same document. <br> 3. Both users make changes simultaneously. |
| *Expected Result*| 1. Edits made by each user should appear in real-time for all collaborators. <br> 2. A collaboration session entry is created in the database with document ID, user IDs, and timestamps. <br> 3. All changes are stored with proper versioning in the database. |
| *Status*         | Pending/Pass/Fail                                             |

### Chai.js Code

```javascript
describe('Real-Time Collaboration', function() {
  it('should sync changes between users in real-time', function() {
    documentPage.openAsUserA();
    documentPage.openAsUserB();
    documentPage.userATypeText('Hello from User A');
    expect(documentPage.userBGetText()).to.include('Hello from User A');
    documentPage.userBTypeText('Hello from User B');
    expect(documentPage.userAGetText()).to.include('Hello from User B');
  });
});
```
## Feature: Document Sharing

| *Test ID*       | *TC-DOC-SHARE-001*                                          |
|--------------------|---------------------------------------------------------------|
| *Description*    | Verify that a document can be shared with another user.      |
| *Precondition*   | User is logged in and has an existing document.              |
| *Steps*          | 1. The user clicks on the "Share" button. <br> 2. The user enters another user's email and grants permissions. <br> 3. The user submits the sharing form. |
| *Expected Result*| 1. The recipient should receive a notification or email with a link to the shared document. <br> 2. A database entry is created with the shared document ID, sender ID, recipient email, and timestamp. |
| *Status*         | Pending/Pass/Fail                                            |

### Chai.js Code

```javascript
describe('Document Sharing', function() {
  it('should share a document successfully', function() {
    documentPage.open();
    documentPage.clickShare();
    documentPage.enterEmail('collaborator@example.com');
    documentPage.grantPermission('Edit');
    documentPage.submitShare();
    expect(documentPage.getShareConfirmation()).to.equal('Document shared successfully');
  });
});
```

## Feature: User Profile Management

| *Test ID*       | *TC-UPM-001*                                               |
|--------------------|--------------------------------------------------------------|
| *Description*    | Verify that the user can successfully update their profile. |
| *Precondition*   | User is logged in.                                          |
| *Steps*          | 1. The user navigates to the profile page. <br> 2. The user updates their profile information (name, email). <br> 3. The user saves the changes. |
| *Expected Result*| 1. The user should see a success message indicating "Profile Updated Successfully." <br> 2. The updated information should reflect on the user's profile. <br> 3. The database entry for the user is updated with the new information and a modification timestamp                 |
| *Status*         | Pending/Pass/Fail                                           |

### Chai.js Code

```javascript
describe('User Profile Management', function() {
  it('should update user profile successfully', function() {
    profilePage.open();
    profilePage.updateProfile('John Updated', 'johnupdated@example.com');
    expect(profilePage.getSuccessMessage()).to.equal('Profile updated successfully');
  });
});
```
## 4. Performance Testing

### Test Case: Concurrent Users
| *Test ID*      | TC-PERF-001                    |
|-------------------|---------------------------------|
| *Description*  | Verify that the system can handle 1,000 concurrent users. |
| *Precondition* | Staging environment is set up. |
| *Steps*        | 1. Simulate 1,000 users concurrently accessing and performing document tasks (viewing, creating, editing documents).<br> 2. Monitor system performance, including response time and resource usage during peak load. <br> 3. Log database queries and actions performed by users to track performance during stress. |
| *Expected Result* | 1. The system remains responsive without errors or crashes, and all user requests are handled successfully.<br> 2. Database operations (e.g., document creation, updates, and retrieval) should complete within an acceptable time frame (e.g., less than 2 seconds per request). <br> 3. Database logs should show no data corruption or loss during concurrent operations, and all session data for 1,000 users should be maintained without conflicts or failures. |
| *Status*       | Pending/Pass/Fail              |

---

## 5. Security Testing

### Test Case: Unauthorized Access
| *Test ID*      | TC-SEC-001                     |
|-------------------|---------------------------------|
| *Description*  | Verify that users without proper roles cannot access admin features. |
| *Precondition* | User is logged in with a non-admin account. |
| *Steps*        | 1. Attempt to access admin-specific URLs or features using a non-admin account.<br> 2. Monitor system behavior to ensure unauthorized users cannot bypass restrictions.<br> 3. Review database logs for unauthorized access attempts.
 | *Expected Result* | 1. The system should deny access to admin features, redirecting users to a "403 Forbidden" or "Access Denied" page.<br> 2. The database should log the unauthorized access attempt, including the user ID, attempted action, and timestamp. <br> 3. No unauthorized changes or modifications should occur in the database, and user roles/privileges should remain unchanged. |
| *Status*       | Pending/Pass/Fail              |

---

## 6. Conclusion

This test plan ensures comprehensive coverage of all functionalities and system requirements. Execution of these test cases will ensure the platform is robust, scalable, and secure.
