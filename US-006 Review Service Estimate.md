# UrbanFleet Operations — Vehicle Service Management Application

## US-006: Review Service Estimate

### Overview
This user story enhances the **Approval** step's interface so that the Customer persona can clearly view the full cost breakdown — Labor Cost, Parts Cost, and the calculated Total Cost — before making an approval decision. It focuses on presentation and readability rather than new data capture, building directly on top of US-003 (estimate generation) and US-004 (approval decision).

---

### Case Type: Vehicle Service Request

**Stage:** `Approval`
**Step:** Approve Service Estimate (enhanced view)
- Same step introduced in US-004, now enriched with a structured, read-only estimate summary section.

---

### Interface Configuration

The approval screen displays the following fields in a clear, structured layout (e.g., a read-only section or table at the top of the approval form):

| Field         | Type     | Description                                  | Editable by Customer |
|----------------|----------|-------------------------------------------------|------------------------|
| Labor Cost     | Currency | Estimated labor charges from inspection/estimate step | No (read-only) |
| Parts Cost     | Currency | Estimated cost of required parts                 | No (read-only) |
| Total Cost     | Currency | Auto-calculated sum of Labor Cost + Parts Cost    | No (read-only) |

- These values are pulled directly from the estimate recorded by the Service Advisor in US-003 — no re-entry or duplication of data.
- Fields are presented as **read-only** to the Customer, since editing the estimate is not part of their role; they only view and decide.
- Layout is structured (e.g., labeled rows or a simple summary table) so costs are easy to scan at a glance rather than buried in a long form.

---

### Persona Access
- **Customer**: Views Labor Cost, Parts Cost, and Total Cost in read-only format, then proceeds to set Approval Status (Approved/Rejected) as configured in US-004.
- **Service Advisor**: No changes — their earlier input (US-003) now flows into this clearer customer-facing view.

---

### Sample Test Case

**Estimate Displayed to Customer:**
- Vehicle ID: UF-2024-0157
- Labor Cost: ₹1,200
- Parts Cost: ₹2,800
- Total Cost: ₹4,000

**Expected Outcome:**
1. Customer opens the Approval assignment.
2. Labor Cost, Parts Cost, and Total Cost are displayed clearly and are non-editable.
3. Customer reviews the breakdown and makes an informed decision (Approved/Rejected) as per US-004.
4. No estimate values are altered by the customer at this step — only viewed.

---

### Tech Stack
- **Platform:** Pega Platform (built via Pega Blueprint)
- **Program:** Pega National Internship Program (NIP)
- **Project:** UrbanFleet Operations — Vehicle Service Management Application

---

### Status
✅ Approval screen updated with structured estimate summary
✅ Labor Cost, Parts Cost, and Total Cost displayed as read-only
✅ Values pulled directly from existing estimate data (no duplication)
✅ Layout verified for clarity and readability
✅ Test case executed end-to-end
