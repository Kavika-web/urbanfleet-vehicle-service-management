# UrbanFleet Operations — Vehicle Service Management Application

## US-001: Submit Vehicle Service Request

### Overview
This user story implements the entry point of the Vehicle Service Management Application. A **Vehicle Service Request** case type captures the initial service request submitted by a customer, validates the required inputs, and links the request to a reusable **Vehicle** data object for consistency across future requests.

---

### Case Type: Vehicle Service Request

Represents the end-to-end lifecycle of a vehicle service request, from initial submission by the customer through to resolution.

**Initial Stage:** `Request Submission`
- Captures request details directly from the Customer persona.
- Acts as the entry point before the case moves into triage/inspection stages.

---

### Properties Captured

| Property           | Type   | Description                                      | Required |
|---------------------|--------|---------------------------------------------------|----------|
| Vehicle ID          | Text   | Unique identifier for the vehicle                  | Yes      |
| Vehicle Model       | Text   | Make/model of the vehicle                          | Yes      |
| Issue Description   | Text   | Customer's description of the problem              | Yes      |

**Validation Rule:** All three properties must be filled in before the case can be submitted. If any required field is missing, submission is blocked and the Customer is prompted to complete the form.

---

### Persona Access
- **Customer**: Can enter Vehicle ID, Vehicle Model, and Issue Description, and submit the request.
- Once submitted, the case becomes available for downstream processing (e.g., inspection, diagnosis, assignment stages in later user stories).

---

### Data Object: Vehicle

A reusable **Vehicle** data object is associated with each Vehicle Service Request case to ensure data consistency across multiple requests for the same vehicle.

**Sample Vehicle Data Object:**
```
Vehicle ID: UF-2024-0157
Make/Model: Tata Ace Gold
Type: Light Commercial Vehicle (Mini Truck)
Registration No: TN-09-AB-4521
Odometer Reading: 42,300 km
Fuel Type: Diesel
Assigned Driver: Ramesh Kumar
Depot/Location: Chennai Central Depot
```

Linking the case to this object means vehicle details (model, registration, depot, etc.) don't need to be re-entered manually each time — they stay consistent and reusable across the application.

---

### Sample Test Case

**Submitted Request:**
- Vehicle ID: UF-2024-0157
- Vehicle Model: Tata Ace Gold
- Issue Description: "Vehicle is experiencing unusual grinding noise from the front-left wheel area during braking, accompanied by a slight pull to the left when brakes are applied. Brake pedal feels softer than usual."

**Expected Outcome:**
1. Customer fills in all three required fields.
2. Validation passes (no fields left blank).
3. Case type `Vehicle Service Request` is created.
4. Case is linked to the Vehicle data object (`UF-2024-0157`).
5. Case moves out of the `Request Submission` stage and becomes available for the next stage of processing.

---

### Tech Stack
- **Platform:** Pega Platform (built via Pega Blueprint)
- **Program:** Pega National Internship Program (NIP)
- **Project:** UrbanFleet Operations — Vehicle Service Management Application

---

### Status
✅ Case type created
✅ Initial stage configured
✅ Properties defined and validated
✅ Vehicle data object linked
✅ Test case executed end-to-end
