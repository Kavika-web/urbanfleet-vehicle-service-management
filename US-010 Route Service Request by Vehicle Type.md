# UrbanFleet Operations — Vehicle Service Management Application

## US-010: Route Service Request by Vehicle Type

### Overview
This user story refines the routing logic within the **Service Execution** stage (US-007) so that cases are directed to one of two dedicated work queues based on the vehicle's type: **HeavyVehicleQueue** for heavy vehicles, and **LightVehicleQueue** for all other types. This ensures technicians see only the cases relevant to their specialization/equipment.

---

### Case Type: Vehicle Service Request

**Stage:** `Service Execution`
- Builds on the auto-assignment step from US-007.
- Instead of routing to a single generic technician queue, the system now evaluates **Vehicle Type** and picks the appropriate queue before assignment.

---

### Routing Logic

**Implementation Options:** When Rule or Decision Table (either is sufficient — no complex escalation needed)

| Vehicle Type            | Routed To            |
|---------------------------|------------------------|
| Heavy Vehicle (e.g., Truck, Bus, Heavy Commercial Vehicle) | `HeavyVehicleQueue`  |
| All other types (e.g., LCV, Pickup, Sedan, Mini Truck)      | `LightVehicleQueue`  |

**Decision Table Example:**
```
IF Vehicle.Type = "Heavy Vehicle" THEN Queue = "HeavyVehicleQueue"
ELSE Queue = "LightVehicleQueue"
```

- The **Vehicle Type** value is read from the linked Vehicle data object (US-005).
- Routing is evaluated automatically as soon as the case enters the Service Execution stage — no manual queue selection by the Service Advisor or Technician.
- This logic sits alongside (or feeds into) the auto-assignment step from US-007, determining *which* queue a technician is auto-assigned from.

---

### Persona Access
- **Technician**: Sees only cases relevant to their queue — HeavyVehicleQueue technicians handle heavy vehicle repairs, LightVehicleQueue technicians handle everything else.
- **Service Advisor / Customer**: No manual involvement — routing is fully automatic and invisible to them.

---

### Sample Test Case

**Case 1 — Light Vehicle:**
- Vehicle ID: UF-2024-0157
- Vehicle Type: Light Commercial Vehicle (Mini Truck)
- **Expected Routing:** LightVehicleQueue

**Case 2 — Heavy Vehicle:**
- Vehicle ID: UF-2024-0512
- Vehicle Type: Heavy Vehicle (Truck)
- **Expected Routing:** HeavyVehicleQueue

**Expected Outcome:**
1. Case enters the Service Execution stage.
2. Decision Table/When Rule evaluates Vehicle Type from the linked Vehicle data object.
3. Case is automatically placed in the correct queue (HeavyVehicleQueue or LightVehicleQueue) with no manual intervention.
4. Technicians only see cases relevant to their assigned queue.

---

### Tech Stack
- **Platform:** Pega Platform (built via Pega Blueprint)
- **Program:** Pega National Internship Program (NIP)
- **Project:** UrbanFleet Operations — Vehicle Service Management Application

---

### Status
✅ Decision Table/When Rule configured for Vehicle Type routing
✅ HeavyVehicleQueue and LightVehicleQueue set up
✅ Automatic routing verified for both vehicle categories
✅ Integrated with existing Service Execution assignment (US-007)
✅ Test case executed end-to-end
