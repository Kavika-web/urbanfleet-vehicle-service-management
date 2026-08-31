# UrbanFleet Operations — Vehicle Service Management Application

## US-008: Notify Service Completion

### Overview
This user story configures a **correspondence mechanism** that automatically notifies the Customer when their service request is resolved. Triggered on case resolution, a Correspondence rule generates a notification containing key service details, keeping the customer informed without manual follow-up.

---

### Case Type: Vehicle Service Request

**Trigger Point:** Case Resolution (end of the case lifecycle, after service execution/repair is completed)
- Fires automatically once the case reaches a resolved status (e.g., "Resolved-Completed").
- No manual action required from the Service Advisor or Technician to send the notification.

---

### Correspondence Rule Configuration

**Rule Type:** Correspondence (Email/Notification)
**Trigger:** On case resolution
**Recipient:** Customer (as captured/linked on the original request)

**Fields Included in Notification:**

| Field            | Description                                         | Source                          |
|--------------------|--------------------------------------------------------|-----------------------------------|
| Case ID           | Unique identifier of the resolved case                  | System (case pyID)                |
| Vehicle ID        | Identifier of the serviced vehicle                       | Vehicle data object (US-005)      |
| Vehicle Model     | Make/model of the vehicle                                 | Vehicle data object (US-005)      |
| Service Summary   | Brief description of work performed                       | Inspection Notes / Technician remarks |
| Total Cost        | Final cost of the service                                 | Estimate (US-003)                 |

---

### Notification Flow

1. Technician marks the repair as complete → Service Status updates → case moves toward resolution.
2. Case reaches resolved status.
3. Correspondence rule fires automatically, compiling Case ID, Vehicle ID, Vehicle Model, Service Summary, and Total Cost into a formatted message.
4. Notification is sent to the Customer (email, or in-app notification depending on channel configuration).

---

### Persona Access
- **Customer**: Receives the notification automatically — no login/action required to trigger it, though they may log in to view full case details.
- **Service Advisor / Technician**: No manual step needed; resolution of the case is what triggers the correspondence.

---

### Sample Test Case

**Case Resolved:**
- Case ID: SR-1042
- Vehicle ID: UF-2024-0157
- Vehicle Model: Tata Ace Gold
- Service Summary: "Replaced front-left brake pads and resurfaced rotor. Brake fluid topped up."
- Total Cost: ₹4,000

**Expected Outcome:**
1. Case status changes to "Resolved-Completed."
2. Correspondence rule triggers automatically.
3. Customer receives a notification containing Case ID (SR-1042), Vehicle ID (UF-2024-0157), Vehicle Model (Tata Ace Gold), Service Summary, and Total Cost (₹4,000).
4. No manual notification step was required from staff.

---

### Tech Stack
- **Platform:** Pega Platform (built via Pega Blueprint)
- **Program:** Pega National Internship Program (NIP)
- **Project:** UrbanFleet Operations — Vehicle Service Management Application

---

### Status
✅ Correspondence rule created and linked to case resolution
✅ Notification triggers automatically on resolve
✅ Case ID, Vehicle ID, Vehicle Model, Service Summary, and Total Cost included in message
✅ Delivery to Customer persona verified
✅ Test case executed end-to-end
