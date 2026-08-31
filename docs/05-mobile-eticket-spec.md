# 📱 Mobile E-Ticket & QR Verification Specification

## 1. Overview
The Mobile E-Ticket interface represents the customer-facing endpoint of the **Movie Ticket Booking Management System**, enabling contactless admission via encoded QR codes.

---

## 2. Dynamic QR Code Payload Structure

The generated QR code contains a cryptographically structured payload:

```json
{
  "booking_id": "M-7",
  "movie": "Avengers: Endgame",
  "theatre": "PVR Inorbit Mall",
  "screen": "Audi 3",
  "show_date": "2026-06-15",
  "show_time": "19:30:00",
  "seats": ["A3", "A4", "A5", "A6", "A7"],
  "total_tickets": 5,
  "status": "CONFIRMED",
  "checksum": "sha256-a9b8c7d6e5f4..."
}
```

---

## 3. UI/UX Layout Specification

* **Header**: Pega Case status badge (`CONFIRMED`), Booking reference `M-7`.
* **Hero Content**: Movie poster banner, Title, Language, Certification (`UA`).
* **Show Information Card**:
  - Theatre complex and hall name (`PVR Inorbit Mall - Audi 3`).
  - Date & Time countdown.
* **Seat Allocation Grid**: Highlighted seat badges (`A3`, `A4`, `A5`, `A6`, `A7`).
* **QR Validation Container**: High-contrast, scannable QR graphic with anti-screenshot security watermark.
* **Price & Tax Breakdown**: Gross ticket amount, GST breakdown, final total (`₹500.00`).
