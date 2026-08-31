# 🧪 Testing, Quality Assurance & Verification Matrix

## 1. Test Strategy Overview

Verification encompasses end-to-end unit, functional, decision-table rule-matching, SLA compliance, and cross-platform responsive testing.

---

## 2. Test Execution Matrix

| Test ID | Test Category | Objective | Inputs | Expected Behavior | Actual Result | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: |
| **TC-001** | Case Creation | Validate case generation and form intake | Movie: *Avengers*, Seats: 5, Email: `test@domain.com` | Case created with ID `M-7`, status `New` | Matches Expected | **PASS** |
| **TC-002** | Pricing Engine | Validate calculation activity accuracy | 5 Tickets @ ₹100.00 each | `TotalBookingCost` = ₹500.00 | Matches Expected | **PASS** |
| **TC-003** | Decision Table | Validate auto-confirmation rule trigger | Tickets = 5, Cost = ₹500.00, EmailSent = true | Returns `Auto Confirm` action | Matches Expected | **PASS** |
| **TC-004** | Case Routing | Validate routing to Premium Desk | Type: *Standard*, Seat Category: *Premium* | Work Object assigned to `Premium Desk` | Matches Expected | **PASS** |
| **TC-005** | SLA Timer | Validate SLA attachment & remaining countdown | Case Creation Timestamp | SLA Goal initialized at 2h, status `On Track` | Matches Expected | **PASS** |
| **TC-006** | Escalation Alert | Validate email notification upon breach | Goal exceeded (> 2 hours) | Escalation email sent to Customer Support Manager | Matches Expected | **PASS** |
| **TC-007** | Data Persistence | Validate state recovery after browser reload | Revisit Case ID `M-7` | Full booking details persisted intact | Matches Expected | **PASS** |
| **TC-008** | Mobile Rendering | Validate responsive E-Ticket view | Mobile User Agent (375x812) | Responsive layout rendered with valid QR code | Matches Expected | **PASS** |

---

## 3. Negative & Boundary Testing

* **Invalid Email**: Rejects submission when email does not conform to RFC 5322.
* **Negative / Zero Tickets**: Form field validation enforces `Minimum value = 1`.
* **Seat Collision**: Concurrency check blocks simultaneous selection of already booked seats.
