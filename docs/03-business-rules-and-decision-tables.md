# ⚡ Business Rules, Decision Tables & Calculation Activities

## 1. Automated Cost Calculation Activity

### Rule Metadata
* **Rule Name**: `Set Total Booking Cost`
* **Rule Type**: `Rule-Obj-Activity`
* **Applies To**: `NIP-MovieTicketBooking-Work-MovieTicketRequest`
* **Purpose**: Calculates the gross booking amount by multiplying ticket quantity with unit seat price.

### Algorithm & Step Sequence
1. **Retrieve Input**: Extract `NumberOfTickets` from primary case page.
2. **Obtain Unit Price**: Access `SelectedShow.TicketPrice` from the linked show data instance.
3. **Execute Formula**:
   $$\text{TotalBookingCost} = \text{NumberOfTickets} \times \text{TicketPrice}$$
4. **Property-Set**: Write resulting value into `.TotalBookingCost`.

```text
Example Calculation:
Ticket Price      : ₹100.00
Number of Tickets : 5
---------------------------------------
Total Booking Cost = 5 * 100.00 = ₹500.00
```

---

## 2. Customer Confirmation Decision Table

### Rule Metadata
* **Rule Name**: `BookingConfirmationDT`
* **Rule Type**: `Rule-Declare-DecisionTable`
* **Applies To**: `NIP-MovieTicketBooking-Work-MovieTicketRequest`

### Decision Logic Table
```text
.-----------------------------------------------------------------------------------------.
| Conditions                                                             | Return Action   |
|------------------------------------------------------------------------+-----------------|
| .NumberOfTickets        | .TotalBookingCost     | .NotificationSent    | .DecisionResult |
|-------------------------+-----------------------+----------------------+-----------------|
| <= 5                    | <= 500.00             | true                 | Auto Confirm    |
| > 5                     | <= 2500.00            | true                 | Standard Queue  |
| Any                     | > 2500.00             | Any                  | Manager Review  |
| Otherwise               | Otherwise             | Otherwise            | Manual Review   |
'-----------------------------------------------------------------------------------------'
```

---

## 3. Smart Routing Decision Table

### Rule Metadata
* **Rule Name**: `Booking Routing DT`
* **Rule Type**: `Rule-Declare-DecisionTable`
* **Applies To**: `NIP-MovieTicketBooking-Work-MovieTicketRequest`

### Routing Matrix
```text
.------------------------------------------------------------------------------------------------------------------.
| # | Booking Type   | Seat Category | Show Timing  | Assignee (Work Queue / Operator) | Notification Channel      |
|---+----------------+---------------+--------------+----------------------------------+---------------------------|
| 1 | Standard       | Regular       | Any          | Booking Team                     | Email (Customer)          |
| 2 | Standard       | Premium       | Any          | Premium Desk                     | Email (Cust), Email (Op)  |
| 3 | Group          | Any           | Any          | Group Booking Team               | Email (Customer), SMS     |
| 4 | Corporate      | Any           | Any          | Corporate Desk                   | Email (Cust), Email (Op)  |
| 5 | Last-minute    | Any           | Next 1 Hour  | Urgent Desk                      | SMS (Customer), Email (Op)|
'------------------------------------------------------------------------------------------------------------------'
```
