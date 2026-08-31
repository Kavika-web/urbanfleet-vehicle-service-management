# UrbanFleet Operations — Vehicle Service Management Application

## US-002: Perform Vehicle Inspection

### Overview
This user story introduces a dedicated **Inspection** stage into the Vehicle Service Request case lifecycle. It allows the Service Advisor persona to record their findings after physically examining the vehicle, and enforces that this step must be completed before the case can move forward to estimate generation.

---

### Case Type: Vehicle Service Request

**Stage:** `Inspection`
- Follows the `Request Submission` stage (US-001).
- Represents the point where a Service Advisor examines the vehicle and logs findings based on the customer's reported issue.
- Acts as a mandatory gate — the case cannot progress to the `Estimate Generation` stage until inspection is completed.

---

### Step Configuration

**Step Name:** Record Inspection Findings
**Persona:** Service Advisor

| Property             | Type          | Description                                              | Required |
|-----------------------|---------------|------------------------------------------------------------|----------|
| Inspection Notes      | Text (Long)   | Detailed observations from the physical inspection          | Yes      |
| Condition Rating       | Dropdown/Pick List | Overall vehicle condition (e.g., Good, Fair, Poor, Critical) | Yes      |

**Validation Rule:** Both Inspection Notes and Condition Rating must be filled in before the Service Advisor can proceed. The case is blocked from advancing to the next stage until this step is marked complete.

---

### Persona Access
- **Service Advisor**: Can view the customer's original request (Vehicle ID, Vehicle Model, Issue Description) and enter Inspection Notes and Condition Rating.
- **Customer**: No access to this stage — inspection is an internal step performed by the service team.

---

### Process Enforcement
- The `Inspection` stage is configured as a required step in the case lifecycle.
- The case cannot transition to `Estimate Generation` (next stage) unless the inspection step is marked complete.
- This ensures the correct sequence: **Request Submission → Inspection → Estimate Generation**, preventing estimates from being generated without a documented inspection.

---

### Sample Test Case

**Inspection Recorded:**
- Vehicle ID: UF-2024-0157 (linked from US-001 request)
- Inspection Notes: "Front-left brake pad worn down to 2mm, rotor shows minor scoring. Brake fluid level slightly low. Recommend pad replacement and rotor resurfacing."
- Condition Rating: Fair

**Expected Outcome:**
1. Service Advisor opens the case and views the linked Vehicle and customer-reported issue.
2. Service Advisor enters Inspection Notes and selects a Condition Rating.
3. Validation passes (both fields filled).
4. Inspection step is marked complete.
5. Case becomes eligible to move into the `Estimate Generation` stage.
6. Attempting to skip ahead to Estimate Generation without completing inspection is blocked.

---

### Tech Stack
- **Platform:** Pega Platform (built via Pega Blueprint)
- **Program:** Pega National Internship Program (NIP)
- **Project:** UrbanFleet Operations — Vehicle Service Management Application

---

### Status
✅ Inspection stage added to case lifecycle
✅ Service Advisor step configured
✅ Inspection Notes and Condition Rating properties defined
✅ Mandatory validation enforced before progression
✅ Test case executed end-to-end
