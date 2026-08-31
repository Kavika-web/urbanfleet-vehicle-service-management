# UrbanFleet Operations — Vehicle Service Management Application

## US-003: Generate Service Estimate

### Overview
This user story adds a second step within the **Inspection** stage, allowing the Service Advisor to generate a service estimate immediately after recording inspection findings. Labor and parts costs are captured, and a **Total Cost** is automatically calculated using a business rule so the estimate is complete and ready for the approval stage.

---

### Case Type: Vehicle Service Request

**Stage:** `Inspection`
**Step:** Generate Service Estimate
- Follows the "Record Inspection Findings" step (US-002) within the same stage.
- Represents the point where the Service Advisor translates inspection findings into a cost estimate for the customer.

---

### Step Configuration

**Persona:** Service Advisor

| Property       | Type     | Description                                                   | Source            |
|-----------------|----------|-----------------------------------------------------------------|--------------------|
| Labor Cost      | Currency | Estimated cost of labor for the repair/service work              | Manual entry       |
| Parts Cost      | Currency | Estimated cost of replacement parts required                     | Manual entry       |
| Total Cost      | Currency (Calculated) | Sum of Labor Cost + Parts Cost                     | Business rule (auto-calculated) |

---

### Business Rule: Total Cost Calculation

A declarative rule (Declare Expression) is configured to automatically compute **Total Cost** whenever Labor Cost or Parts Cost changes:

```
Total Cost = Labor Cost + Parts Cost
```

- The calculation runs automatically — no manual entry or button click required.
- The result is stored on the case, so it persists and is visible to downstream stages (e.g., Approval).
- If either Labor Cost or Parts Cost is updated later, Total Cost recalculates immediately to stay in sync.

---

### Persona Access
- **Service Advisor**: Enters Labor Cost and Parts Cost; Total Cost is read-only and system-generated.
- **Customer**: No access to this step — estimate generation is an internal process.

---

### Sample Test Case

**Estimate Generated (following US-002 inspection):**
- Vehicle ID: UF-2024-0157
- Inspection Notes: "Front-left brake pad worn down to 2mm, rotor shows minor scoring."
- Labor Cost: ₹1,200
- Parts Cost: ₹2,800
- Total Cost: ₹4,000 *(auto-calculated)*

**Expected Outcome:**
1. Service Advisor enters Labor Cost and Parts Cost after completing inspection.
2. Total Cost field updates automatically to reflect the sum, with no manual input.
3. The estimate (Labor Cost, Parts Cost, Total Cost) is saved to the case.
4. The case is now ready to move into the Approval stage with a complete, accurate estimate available for review.

---

### Tech Stack
- **Platform:** Pega Platform (built via Pega Blueprint)
- **Program:** Pega National Internship Program (NIP)
- **Project:** UrbanFleet Operations — Vehicle Service Management Application

---

### Status
✅ Estimate generation step added within Inspection stage
✅ Labor Cost and Parts Cost properties configured
✅ Total Cost calculated automatically via business rule
✅ Estimate persists on case for downstream approval review
✅ Test case executed end-to-end
