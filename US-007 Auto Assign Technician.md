# UrbanFleet Operations — Vehicle Service Management Application

## US-007: Auto Assign Technician

### Overview
This user story introduces a **Service Execution** stage to handle the actual fulfilment of approved service requests. It adds an automated assignment step that routes the case to a Technician (or technician work queue) without manual intervention, and tracks the assignment via case properties.

---

### Case Type: Vehicle Service Request

**Stage:** `Service Execution`
- Follows the `Approval` stage (US-004), and is only reached when Approval Status = **Approved**.
- Represents the beginning of hands-on repair/service work.

---

### Step Configuration

**Step Name:** Auto Assign Technician
**Routing Type:** System-driven (Automatic), no Customer or Service Advisor input required

| Property             | Type   | Description                                              | Set By          |
|------------------------|--------|--------------------------------------------------------------|-------------------|
| Assigned Technician    | Text/Reference | The technician (or work queue) the case is routed to     | System (automatic) |
| Service Status         | Pick List | Current status of service work (e.g., Assigned, In Progress, Completed) | System (auto-set to "Assigned" initially) |

---

### Assignment Logic

- Upon entering the `Service Execution` stage, the system automatically assigns the case to:
  - A **Technician persona/work queue** based on availability, workload, or depot/location, or
  - A shared **Technician work queue**, where any available technician can pick up the case.
- No manual routing step is required from the Service Advisor or Customer — assignment happens as soon as the case enters this stage.
- **Assigned Technician** is populated automatically once routing completes.
- **Service Status** is set to "Assigned" to reflect that the case is now with the service execution team.

---

### Persona Access
- **Technician**: Receives the case in their worklist/queue once auto-assigned; can view inspection notes, estimate, and vehicle details to begin repair work.
- **Service Advisor / Customer**: No action required at this step — visibility only, to track that assignment has occurred.

---

### Sample Test Case

**Case Entering Service Execution:**
- Vehicle ID: UF-2024-0157
- Approval Status: Approved (from US-004)

**Expected Outcome:**
1. Case automatically transitions into the `Service Execution` stage after approval.
2. System auto-assigns the case to a Technician (e.g., "Technician: Arun Vel" or "Technician Work Queue: Chennai Central Depot").
3. Assigned Technician property is populated without manual input.
4. Service Status updates to "Assigned."
5. Case appears in the assigned technician's worklist, ready for repair to begin.

---

### Tech Stack
- **Platform:** Pega Platform (built via Pega Blueprint)
- **Program:** Pega National Internship Program (NIP)
- **Project:** UrbanFleet Operations — Vehicle Service Management Application

---

### Status
✅ Service Execution stage added to case lifecycle
✅ Automatic assignment step configured (Technician/work queue)
✅ Assigned Technician and Service Status properties tracked
✅ Assignment verified to occur without manual routing
✅ Test case executed end-to-end
