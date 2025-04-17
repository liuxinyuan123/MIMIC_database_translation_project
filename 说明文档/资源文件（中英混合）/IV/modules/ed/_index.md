# ED module
The ED module contains data for emergency department patients collected while they are in the ED. Information includes reason for admission, triage assessment, vital signs, and medicine reconciliaton. The `subject_id` and `hadm_id` identifiers allow MIMIC-IV-ED to be linked to other MIMIC-IV modules.

----

## [diagnosis](./diagnosis.md) table


- The *[diagnosis](./diagnosis.md)* table provides billed diagnoses for patients. Diagnoses are 
determined after discharge from the emergency department.


## [edstays](./edstays.md) table
- The *[edstays](./edstays.md)* table is the primary tracking table for 
emergency department visits.
- It provides the time the patient entered the emergency department and the 
  time they left the emergency department.


## [medrecon](./medrecon.md) table
- On admission to the emergency departments, staff will ask the patient what 
current medications they are taking. This process is called medicine reconciliation, and the *[medrecon](./medrecon.md)* table stores the findings of the care providers.

## [pyxis](./pyxis.md) table
- The *[pyxis](./pyxis.md)* table provides information for medicine 
dispensations made via the Pyxis system.

- Note that as the same medication may have multiple `gsn` values, each row 
does *not* necessarily indicate a unique dispensation. The `med_rn` column allows for subselecting to individual dispensations.


## [triage](./triage.md) table
- The *[triage](./triage.md)* table contains information about the patient 
  when they were 
first triaged in the emergency department.
Patients are assessed at triage by a single care provider and asked a series of questions to assess their current health status.
Their vital signs are measured and a level of acuity is assigned. Based on the level of acuity, the patient either waits in the waiting room for later attention, or is prioritized for immediate care.

## [vitalsign](./vitalsign.md) table
- Patients admitted to the emergency department have routine vital signs 
taken ever 1-4 hours. These vital signs are stored in the *[vitalsign](./vitalsign.md)* table.
