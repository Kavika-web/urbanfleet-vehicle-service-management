# UrbanFleet Operations — Vehicle Service Management Application

## US-005: Maintain Vehicle Data

### Overview
This user story establishes a **reusable Vehicle data object**, decoupled from the Vehicle Service Request case type. Storing vehicle information independently allows the same vehicle record to be referenced across multiple service requests over time, ensuring data consistency and enabling a full service history to be tracked per vehicle.

---

### Data Object: Vehicle

**Type:** Reusable Data Object (Data Class, not a Case Type)
- Exists independently of any single case.
- Can be created once per vehicle and referenced by any number of Vehicle Service Request cases going forward.

| Property     | Type   | Description                                        | Required |
|---------------|--------|-------------------------------------------------------|----------|
| Vehicle ID    | Text   | Unique identifier for the vehicle                      | Yes      |
| Model         | Text   | Make/model of the vehicle                              | Yes      |
| Type          | Text/Pick List | Vehicle category (e.g., LCV, Pickup, Sedan, Truck) | Yes      |

---

### Association with Vehicle Service Request

- Each Vehicle Service Request case includes a reference (embedded page or linked data page) to a Vehicle data object.
- When a customer submits a request (US-001), the system either:
  - Links to an **existing** Vehicle record (if the Vehicle ID already exists), or
  - Creates a **new** Vehicle record (if it's the vehicle's first service request).
- This means vehicle details (Model, Type) don't need to be re-entered on every request — they're pulled from the shared data object.

---

### Benefits of This Design

- **Consistency:** Vehicle Model and Type are stored once and reused, avoiding mismatched or duplicate entries across requests for the same vehicle.
- **Service History Tracking:** Since multiple Vehicle Service Request cases can reference the same Vehicle record, all past requests, inspections, and repairs for that vehicle can be traced back to a single source.
- **Scalability:** As the fleet grows, new vehicles are simply added as new data object instances without altering the case type structure.

---

### Sample Test Case

**Vehicle Data Object:**
```
Vehicle ID: UF-2024-0157
Model: Tata Ace Gold
Type: Light Commercial Vehicle (Mini Truck)
```

**Expected Outcome:**
1. Vehicle record `UF-2024-0157` is created once in the Vehicle data object.
2. A Vehicle Service Request case (US-001) is submitted and linked to this Vehicle record.
3. A second, later service request for the same vehicle (e.g., 3 months later) also links to the same Vehicle record instead of creating a duplicate.
4. Querying the Vehicle record shows all associated Vehicle Service Request cases, giving a consolidated service history.

---

### Tech Stack
- **Platform:** Pega Platform (built via Pega Blueprint)
- **Program:** Pega National Internship Program (NIP)
- **Project:** UrbanFleet Operations — Vehicle Service Management Application

---

### Status
✅ Vehicle data object created (independent of case type)
✅ Vehicle ID, Model, Type properties defined
✅ Association with Vehicle Service Request case configured
✅ Reusability across multiple requests verified
✅ Test case executed end-to-end
