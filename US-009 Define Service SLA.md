# UrbanFleet Operations — Vehicle Service Management Application

## US-009: Define Service SLA

### Overview
This user story configures a simple **Service Level Agreement (SLA)** on the Vehicle Service Request case type to ensure requests are handled within a reasonable timeframe. It sets a Goal and a Deadline measured from case creation, with automatic urgency handling when each is missed — no complex multi-step escalation chains required.

---

### Case Type: Vehicle Service Request

**SLA Applied At:** Case level (applies across the full lifecycle, from creation to resolution)

---

### SLA Configuration

| Setting     | Duration              | Behavior on Miss                                   |
|--------------|------------------------|--------------------------------------------------------|
| Goal         | 2 days from case creation | Case is flagged as **approaching deadline**             |
| Deadline     | 3 days from case creation | Case **priority is automatically increased**             |

- Both Goal and Deadline are timed from the case's **Create Date/Time**.
- This is a straightforward interval-based SLA — no custom escalation activities, additional notifications, or multi-tier urgency rules are configured.

---

### Behavior Details

**When Goal (2 days) is missed:**
- The case is visually/logically flagged as approaching its deadline (e.g., urgency value increases, or a status indicator changes).
- This acts as an early warning to whoever owns the case (Service Advisor/Technician) that action is needed soon.

**When Deadline (3 days) is missed:**
- The system automatically increases the case's **priority/urgency value**.
- This pushes the case higher in worklists, making it more visible for the assigned persona to act on.

---

### Persona Impact
- **Service Advisor / Technician**: See cases with increased urgency rise to the top of their worklist once the goal or deadline is breached, prompting faster action.
- **Customer**: No direct visibility into SLA mechanics — benefits indirectly through faster handling of delayed requests.

---

### Sample Test Case

**Case Created:**
- Case ID: SR-1042
- Vehicle ID: UF-2024-0157
- Created: 28-Aug-2026, 10:00 AM

**Expected Outcome:**
1. **Goal check (30-Aug-2026, 10:00 AM):** If the case is still open, it is flagged as approaching deadline.
2. **Deadline check (31-Aug-2026, 10:00 AM):** If the case is still open, its priority is automatically increased, making it more prominent in the assigned worklist.
3. If the case is resolved before 2 days, no flag or priority change occurs — SLA is met.

---

### Tech Stack
- **Platform:** Pega Platform (built via Pega Blueprint)
- **Program:** Pega National Internship Program (NIP)
- **Project:** UrbanFleet Operations — Vehicle Service Management Application

---

### Status
✅ SLA configured on Vehicle Service Request case type
✅ Goal set to 2 days from case creation
✅ Deadline set to 3 days from case creation
✅ Goal-miss flagging behavior verified
✅ Deadline-miss automatic priority increase verified
✅ Test case executed end-to-end
