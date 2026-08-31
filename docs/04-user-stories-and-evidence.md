# 🎯 User Story Specifications & Runtime Evidence (US-001 – US-010)

This document provides a comprehensive technical breakdown of all 10 user stories implemented in the **Movie Ticket Booking Management System**, mapped directly to runtime validation evidence.

---

### 📌 US-001: Submit Movie Ticket Booking Request
* **User Story**: *As a customer, I want to select my preferred movie, theatre, show date/time, ticket count, and seats, and provide my contact details so that I can submit a ticket booking request.*
* **Acceptance Criteria**:
  - The UI captures Movie, Theatre, Show Date, Show Time, Tickets, Seat Preference, Customer Name, Email, and Phone Number.
  - Submitting creates a new Case instance with an auto-incremented Case ID (`M-7`).
  - Lifecycle transitions to `Booking Review` stage.
* **Runtime Verification**:
  ![US-001 Evidence](../Screenshots/US-001.png)

---

### 📌 US-002: Review Booking Summary
* **User Story**: *As a customer, I want to view a consolidated summary of my booking before final confirmation so that I can verify all details.*
* **Acceptance Criteria**:
  - Read-only review section displaying Movie (`Avengers: Endgame`), Theatre (`PVR Inorbit Mall`), Date (`15/06/2026`), Time (`07:30 PM`), Seats (`A3, A4, A5, A6, A7`), Tickets (`5`), and Total Cost (`₹500.00`).
* **Runtime Verification**:
  ![US-002 Evidence](../Screenshots/US-002.png)

---

### 📌 US-003: Evaluate Customer Confirmation Decision Table
* **User Story**: *As a system, I want to evaluate booking parameters against configured business rules using a Pega Decision Table to automate decision outcomes.*
* **Acceptance Criteria**:
  - Decision table evaluates `Number of Tickets` (`5`), `Total Booking Cost` (`₹500.00`), and `Notification Email Sent` (`true`).
  - Matches rule and returns `Auto Confirm` outcome.
* **Runtime Verification**:
  ![US-003 Evidence](../Screenshots/US-003.png)

---

### 📌 US-004: Confirm Booking & Status Management
* **User Story**: *As a customer, I want to receive an immediate booking confirmation with a final status of Confirmed.*
* **Acceptance Criteria**:
  - Case status `pyStatusWork` transitions to `Resolved-Completed` / `Confirmed`.
  - Confirmation screen shows Booking ID `M-7`, formatted summary, and confirmation timestamp.
* **Runtime Verification**:
  ![US-004 Evidence](../Screenshots/US-004.png)

---

### 📌 US-005: View Confirmed Booking Record Persistence
* **User Story**: *As an auditor/customer, I want the confirmed booking record to persist accurately across sessions.*
* **Acceptance Criteria**:
  - Data integrity maintained upon reopening the case.
  - Notification alert indicates that the E-Ticket has been dispatched to the customer's registered email.
* **Runtime Verification**:
  ![US-005 Evidence](../Screenshots/US-005.png)

---

### 📌 US-006: Omnichannel Mobile E-Ticket with QR Code
* **User Story**: *As a mobile user, I want to view a responsive mobile E-Ticket with a dynamic QR code for quick check-in at the theatre entrance.*
* **Acceptance Criteria**:
  - Mobile viewport optimization.
  - Renders Booking ID, Movie, Screen, Showtime, Seats, Total, and scannable QR Code.
* **Runtime Verification**:
  ![US-006 Evidence](../Screenshots/US-006.png)

---

### 📌 US-007: Maintain Movie / Theatre Master Data
* **User Story**: *As an administrator, I want reusable data objects for Movies, Theatres, and Shows so that booking cases can dynamically reference master records.*
* **Acceptance Criteria**:
  - Configured `Data-Movie`, `Data-Theatre`, and `Data-Show` in Dev Studio.
  - Relational lookups link Shows to Movies and Theatres.
* **Runtime Verification**:
  ![US-007 Evidence](../Screenshots/US-007.png)

---

### 📌 US-008: Calculate Total Booking Cost
* **User Story**: *As a business analyst, I want the system to calculate the total booking cost automatically as `Number of Tickets * Ticket Price`.*
* **Acceptance Criteria**:
  - Calculation activity `Set Total Booking Cost` executes during case processing.
  - Dynamically computes and sets `TotalBookingCost`.
* **Runtime Verification**:
  ![US-008 Evidence](../Screenshots/US-008.png)

---

### 📌 US-009: Service Level Agreement (SLA) Configuration
* **User Story**: *As an operations manager, I want an SLA rule configured on booking requests with goal/deadline timelines and automated escalation.*
* **Acceptance Criteria**:
  - SLA `Movie Ticket Request SLA` configured with **Goal: 2 hours** and **Deadline: 2 hours**.
  - Escalation email automatically dispatched to `Customer Support Manager` if goal is violated.
  - Case displays runtime SLA tracker (`On Track: 1h 20m remaining`).
* **Runtime Verification**:
  ![US-009 Evidence](../Screenshots/US-009.png)

---

### 📌 US-010: Smart Routing & Notification Matrix
* **User Story**: *As a customer support lead, I want cases intelligently routed to specific work queues and multi-channel notifications sent to customers and operators.*
* **Acceptance Criteria**:
  - Decision Table `Booking Routing DT` assigns case `M-7` to `Premium Desk`.
  - Notification templates generate tailored email and SMS messages.
* **Runtime Verification**:
  ![US-010 Evidence](../Screenshots/US-010.png)
