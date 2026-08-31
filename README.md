# 🎬 Movie Ticket Booking Management System

<div align="center">

[![Pega Platform](https://img.shields.io/badge/Pega_Platform-8.x_%7C_App_Studio_%7C_Dev_Studio-263238?style=for-the-badge&logo=pega&logoColor=white)](https://www.pega.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](./LICENSE)
[![Author](https://img.shields.io/badge/Author-Rajkaran_Yadav-007ACC?style=for-the-badge&logo=github)](https://github.com/Rajkaran-122)
[![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)]()
[![Build](https://img.shields.io/badge/Architecture-Enterprise_BPM-orange?style=for-the-badge)]()

**An enterprise-grade, end-to-end Pega Case Management Application automating the complete movie ticket booking lifecycle—from user request and data validation to automated decision-table evaluation, SLA tracking, smart routing, and dynamic mobile E-Ticket generation with QR check-in.**

[Key Features](#-key-features) • [Application Architecture](#-application-architecture) • [User Stories & Evidence](#-user-stories--evidence-us-001--us-010) • [Data Model](#-data-model) • [Decision Logic](#-business-rules--decision-logic) • [Documentation](#-project-documentation) • [Author](#-author--contact)

---

</div>

## 📌 Executive Summary

The **Movie Ticket Booking Management System** is a business-process automation application built on the **Pega Platform**. It streamlines ticket reservations by capturing cinema, showtime, customer, and seat inventory details, evaluating business rules via **Pega Decision Tables**, enforcing compliance with **Service Level Agreements (SLAs)**, and routing cases intelligently across desks.

### 🌟 Highlights
- **Case Type**: `Movie Ticket Request` (Sample Case Prefix: `M-`)
- **Automated Decision Engine**: Zero-touch auto-confirmation for compliant bookings based on ticket counts and cost thresholds.
- **Dynamic Cost Calculation**: Automated Pega activity calculating total price dynamically (`Tickets × Show Price`).
- **SLA & Escalation Protocol**: 2-hour Goal & Deadline with automated escalation email triggers to the Customer Support Manager.
- **Role-Based Smart Routing**: Intelligent case routing across Standard, Premium, Group, Corporate, and Urgent desks.
- **Omnichannel Mobile E-Ticket**: Responsive customer confirmation with dynamic QR code generation for theatre entry.

---

## 🏗️ Application Architecture & Lifecycle

```mermaid
flowchart TD
    subgraph STAGE1["Stage 1: Movie Ticket Request"]
        A[Customer Submits Booking Form] --> B[Capture Movie, Theatre, Show, Seats & Contact]
    end

    subgraph STAGE2["Stage 2: Booking Review"]
        B --> C[Fetch Master Show & Pricing Data]
        C --> D[Execute Activity: Calculate Total Cost]
        D --> E[Present Consolidated Summary to Customer]
    end

    subgraph STAGE3["Stage 3: Decision & Routing Evaluation"]
        E --> F[Pega Decision Table: Evaluate Conditions]
        F -->|Eligible: Tickets <= 5, Cost <= 500| G[Auto Confirm Outcome]
        F -->|Non-Standard / Exception| H[Smart Routing to Support Desk]
    end

    subgraph STAGE4["Stage 4: Booking Confirmation & SLA"]
        G --> I[Set Case Status: Resolved-Completed]
        H --> I
        I --> J[Monitor SLA: 2h Goal / Escalation Trigger]
    end

    subgraph STAGE5["Stage 5: Mobile E-Ticket & Check-in"]
        J --> K[Generate Customer Record]
        K --> L[Emit Notification Email / SMS]
        L --> M[Issue Mobile E-Ticket with QR Code Check-in]
    end

    style STAGE1 fill:#f0f4ff,stroke:#2b6cb0,stroke-width:2px
    style STAGE2 fill:#f0fff4,stroke:#276749,stroke-width:2px
    style STAGE3 fill:#fffaf0,stroke:#dd6b20,stroke-width:2px
    style STAGE4 fill:#fdf2f8,stroke:#97266d,stroke-width:2px
    style STAGE5 fill:#f7fafc,stroke:#4a5568,stroke-width:2px
```

---

## 📸 User Stories & Evidence (US-001 – US-010)

The application has been verified across all 10 core enterprise user stories with runtime execution evidence.

### 🔹 US-001: Submit Movie Ticket Booking Request
* **Goal**: Enable customers to choose movies, theatres, show timings, seat counts, seat preferences, and submit contact information.
* **Result**: Initializes case `M-7` and advances case lifecycle to the review stage.

![US-001 Evidence](Screenshots/US-001.png)

---

### 🔹 US-002: Review Booking Summary
* **Goal**: Display consolidated booking details (Movie, Theatre, Date, Time, Seat Selection, Ticket Count, and calculated Total Cost) before payment/decision.
* **Result**: Clean summary view allowing users to confirm details accurately.

![US-002 Evidence](Screenshots/US-002.png)

---

### 🔹 US-003: Evaluate Customer Confirmation Decision Table
* **Goal**: Automate booking eligibility evaluation using declarative decision tables (`Number of Tickets`, `Total Booking Cost`, `Notification Sent`).
* **Result**: Instant rule-matched outcome returning `Auto Confirm`.

![US-003 Evidence](Screenshots/US-003.png)

---

### 🔹 US-004: Confirm Booking & Update Work Status
* **Goal**: Finalize booking, transition case status (`pyStatusWork`) to `Resolved-Completed`, and present confirmation details.
* **Result**: Case `M-7` successfully confirmed with timestamp.

![US-004 Evidence](Screenshots/US-004.png)

---

### 🔹 US-005: View Confirmed Booking Record & Persistence
* **Goal**: Guarantee auditability and data persistence when case records are revisited.
* **Result**: Verified persistence of transaction data and dispatch of email notifications.

![US-005 Evidence](Screenshots/US-005.png)

---

### 🔹 US-006: Omnichannel Mobile E-Ticket with QR Code
* **Goal**: Deliver a responsive, mobile-optimized E-Ticket containing booking ID, screen, seat allocation, and a scannable QR code for entry validation.
* **Result**: High-fidelity mobile customer portal with instant check-in readiness.

<div align="center">
  <img src="Screenshots/US-006.png" alt="US-006 Mobile E-Ticket" width="420" />
</div>

---

### 🔹 US-007: Maintain Movie, Theatre & Show Data Objects
* **Goal**: Design relational data structures in Dev Studio for `Movie`, `Theatre`, and `Show` master records referenced dynamically by booking cases.
* **Result**: Reusable data layer with primary keys and dynamic lookups.

![US-007 Evidence](Screenshots/US-007.png)

---

### 🔹 US-008: Automated Total Booking Cost Calculation
* **Goal**: Implement a Pega calculation Activity (`Set Total Booking Cost`) executing `Total Cost = Number of Tickets * Ticket Price`.
* **Result**: Real-time automatic computation across all case steps.

![US-008 Evidence](Screenshots/US-008.png)

---

### 🔹 US-009: Service Level Agreement (SLA) & Escalation Matrix
* **Goal**: Enforce a 2-hour Goal and 2-hour Deadline SLA with automated escalation notifications to the Customer Support Manager.
* **Result**: SLA monitoring active with real-time countdown (`On Track: 1h 20m remaining`).

![US-009 Evidence](Screenshots/US-009.png)

---

### 🔹 US-010: Smart Routing & Notification Matrix
* **Goal**: Route cases to dedicated operational desks (Standard, Premium Desk, Group, Corporate Desk, Urgent Desk) and trigger dual-channel notifications.
* **Result**: Case `M-7` auto-routed to `Premium Desk` with automated customer and assignee alerts.

![US-010 Evidence](Screenshots/US-010.png)

---

## 📊 Data Model & Entity Specifications

The application uses structured Pega Data Types configured in Dev Studio:

```
                  ┌──────────────────────┐
                  │      Data-Movie      │
                  ├──────────────────────┤
                  │ Movie ID (PK)        │
                  │ Movie Name           │
                  │ Genre                │
                  │ Language             │
                  │ Duration (mins)      │
                  │ Rating               │
                  │ Status               │
                  └──────────┬───────────┘
                             │
                             │ references
                             ▼
┌─────────────────────┐   ┌──────────────────────┐   ┌───────────────────────────┐
│    Data-Theatre     │   │      Data-Show       │   │ Work-MovieTicketRequest   │
├─────────────────────┤   ├──────────────────────┤   ├───────────────────────────┤
│ Theatre ID (PK)     │◀──┤ Show ID (PK)         │◀──┤ Case ID (e.g., M-7)       │
│ Theatre Name        │   │ Movie (Reference)    │   │ Show ID (Lookup)          │
│ Location            │   │ Theatre (Reference)  │   │ Customer Name, Email, Ph  │
│ City                │   │ Show Date            │   │ Seats Allocated           │
│ Total Screens       │   │ Show Time            │   │ Number of Tickets         │
│ Contact Number      │   │ Screen               │   │ Total Booking Cost (Calc) │
│ Status              │   │ Ticket Price (Curr)  │   │ pyStatusWork              │
└─────────────────────┘   │ Available Seats      │   │ SLA Goal & Escalation     │
                          │ Status               │   │ Routing Assignee          │
                          └──────────────────────┘   └───────────────────────────┘
```

---

## ⚙️ Business Rules & Decision Logic

### 1. Booking Evaluation Decision Table
| Condition: Tickets | Condition: Total Cost | Condition: Email Sent | Return Action |
| :--- | :--- | :--- | :--- |
| `<= 5` | `<= ₹500.00` | `true` | **`Auto Confirm`** |
| `> 5` | `Any` | `Any` | `Manual Review Desk` |
| `Any` | `> ₹2500.00` | `Any` | `Manager Approval` |
| `Otherwise` | `Otherwise` | `Otherwise` | `Standard Processing` |

### 2. Case Routing Decision Matrix
| Booking Type | Seat Category | Show Timing | Assigned Queue / Desk | Notification Channels |
| :--- | :--- | :--- | :--- | :--- |
| **Standard** | Regular | Any | `Booking Team` | Email (Customer) |
| **Standard** | Premium | Any | `Premium Desk` | Email (Customer), Email (Assignee) |
| **Group** | Any | Any | `Group Booking Team`| Email (Customer), SMS |
| **Corporate** | Any | Any | `Corporate Desk` | Email (Customer), Email (Assignee) |
| **Last-minute** | Any | `< 1 Hour` | `Urgent Desk` | SMS (Customer), Email (Assignee) |

---

## 📚 Project Documentation

For deep technical insights, explore the dedicated documentation modules:

- 📖 [**01. Project Architecture & Data Model**](docs/01-architecture-and-data-model.md)
- 🔄 [**02. Case Lifecycle & Stage Workflows**](docs/02-case-lifecycle-and-workflows.md)
- ⚡ [**03. Decision Tables & Calculation Rules**](docs/03-business-rules-and-decision-tables.md)
- 🎯 [**04. User Story Technical Specifications**](docs/04-user-stories-and-evidence.md)
- 📱 [**05. Omnichannel Mobile E-Ticket Specification**](docs/05-mobile-eticket-spec.md)
- 🧪 [**06. Test Cases & Verification Matrix**](docs/06-testing-and-validation.md)

---

## 🛠️ Verification & Test Matrix

| Test ID | Test Scenario | Input Data | Expected Output | Status |
| :--- | :--- | :--- | :--- | :---: |
| **TC-01** | Valid standard booking creation | 5 Tickets, PVR Inorbit, ₹500 | Case `M-7` generated in `Booking Review` | `PASSED` |
| **TC-02** | Automatic cost calculation | 5 Tickets × ₹100.00 | Total Cost evaluated to ₹500.00 | `PASSED` |
| **TC-03** | Decision table auto-confirmation | Tickets `<= 5`, Cost `<= 500` | Outcome returned as `Auto Confirm` | `PASSED` |
| **TC-04** | SLA attachment & deadline tracking | Case created | 2h Goal & Deadline attached with active countdown | `PASSED` |
| **TC-05** | Smart routing to Premium Desk | Standard type + Premium seats | Case routed to `Premium Desk` queue | `PASSED` |
| **TC-06** | Mobile E-Ticket render | Valid confirmed case | QR check-in and responsive layout visible | `PASSED` |

---

## 👨‍💻 Author & Contact

**Rajkaran Yadav**  
- **GitHub**: [@Rajkaran-122](https://github.com/Rajkaran-122)  
- **Email**: [yadavrajkaran854@gmail.com](mailto:yadavrajkaran854@gmail.com)  
- **Role**: Pega Application Developer & Solution Architect  

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

```text
Copyright (c) 2026 Rajkaran Yadav <yadavrajkaran854@gmail.com>
```
