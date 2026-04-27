# Requirement: Phone Number CRUD Application

## Project Overview
A simple web application for storing and managing personal or business contact phone numbers.  
Users should be able to create, view, edit, and delete contact entries, each containing a name and a phone number.

## Target Platform
Web (Next.js + NestJS + SQLite)

## Functional Requirements

### 1. Contact List Page
- Display all saved contacts in a table or card list.
- Each entry shows the contact name and phone number.
- Provide a button to add a new contact.
- Provide options to edit or delete each contact.

### 2. Add New Contact
- A form with fields for name (text, required) and phone number (tel, required, must be valid).
- After submission, save to database and redirect to the contact list.
- Show success or error messages appropriately.

### 3. Edit Contact
- Clicking "Edit" on a contact navigates to a pre‑filled form.
- Fields: name and phone number, same validation as creation.
- Save updates the existing record and returns to the list.

### 4. Delete Contact
- Clicking "Delete" shows a confirmation dialog.
- After confirmation, the contact is permanently removed and the list updates.

### 5. Validation
- Name cannot be empty or exceed 100 characters.
- Phone number must be a valid Thai mobile or landline format (10 digits, starts with 0).
- Duplicate phone numbers are not allowed (unique constraint).

## Non‑Functional Requirements
- The backend API should use REST (OpenAPI 3.0) and JSON.
- The frontend must be responsive and usable on mobile browsers.
- All responses must be in Thai language.
- The application must be usable without authentication (public, single‑user).
- No pagination needed if total contacts are under a few hundred.

## User Stories
1. As a user, I want to see all my saved contacts so that I can quickly find a number.
2. As a user, I want to add a new contact with a name and phone number.
3. As a user, I want to edit an existing contact if details change.
4. As a user, I want to delete a contact I no longer need.
5. As a user, I want to be warned if I try to enter an invalid phone number or duplicate entry.

## Acceptance Criteria
- Given I am on the contact list, when I click "Add Contact", then a form appears. After filling valid data and submitting, the new contact appears at the top of the list.
- Given I click "Edit" on a contact, when I change the name and save, then the updated name reflects in the list.
- Given I click "Delete" and confirm, the contact disappears from the list and is no longer available via API.
- Given I try to submit a form with an empty name or invalid phone, an error message is shown and the data is not saved.
- Given I try to add a phone number that already exists, an error message "This phone number is already in use" is displayed.