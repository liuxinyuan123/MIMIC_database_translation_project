
  The Hosp module provides all data acquired from the hospital wide electronic health record. Information covered includes patient and admission information, laboratory measurements, microbiology, medication administration, and billed diagnoses.
  
-----

The hosp module contains data derived from the hospital wide EHR. These measurements are predominantly recorded during the hospital stay, though some tables include data from outside the hospital as well (e.g. outpatient laboratory tests in _**labevents**_).

### Information includes patient and admission details

- **_[patients](./patients.md)_**
- **_[admissions](./admissions.md)_**
- **_[transfers](./transfers.md)_**


### laboratory measurements
- **_[labevents](./labevents.md)_**
- **_[d_labitems](./d_labitems.md)_**


### microbiology cultures 
- **_[microbiologyevents](./microbiologyevents.md)_**


###  orders
- **_[poe](./poe.md)_**
- **_[poe_detail](./poe_detail.md)_**


### medication administration 
- **_[emar](./emar.md)_**
- **_[emar_detail](./emar_detail.md)_**

### medication prescription 
- **_[prescriptions](./prescriptions.md)_**
- **_[pharmacy](./pharmacy.md)_**

### hospital billing information 
- **_[diagnoses_icd](./diagnoses_icd.md)_**
- **_[d_icd_diagnoses](./d_icd_diagnoses.md)_**
- **_[procedures_icd](./procedures_icd.md)_**
- **_[d_icd_procedures](./d_icd_procedures.md)_**
- **_[hcpcsevents](./hcpcsevents.md)_**
- **_[d_hcpcs](./d_hcpcs.md)_**
- **_[drgcodes](./drgcodes.md)_**


### hospital service related information 
- **_[services](./services.md)_**


### Hosp

#### [omr ](./omr.md)table  
The Online Medical Record (OMR) table contains miscellaneous information from the EHR.

#### [provider](./provider.md) table   

The provider table lists deidentified provider identifiers used in the database.


#### [admissions](./admissions.md) table

Detailed information about hospital stays.

#### [d_hcpcs](./d_hcpcs.md) table 
Dimension table for hcpcsevents; provides a description of CPT codes.

#### [d_icd_diagnoses](./d_icd_diagnoses.md) table 
Dimension table for diagnoses_icd; provides a description of ICD-9/ICD-10 billed diagnoses.

####   [d_icd_procedures](./d_icd_procedures.md) table 
Dimension table for procedures_icd; provides a description of ICD-9/ICD-10 billed procedures.

#### [d_labitems](./d_labitems.md)
Dimension table for labevents provides a description of all lab items.

#### [diagnoses_icd](./diagnoses_icd.md)
Billed ICD-9/ICD-10 diagnoses for hospitalizations.

#### [drgcodes](./drgcodes.md)
Billed diagnosis related group (DRG) codes for hospitalizations.

#### [emar](./emar.md)
The Electronic Medicine Administration Record (eMAR); barcode scanning of medications at the time of administration.

#### [emar_detail](./emar_detail.md)
Supplementary information for electronic administrations recorded in emar.

#### [hpcsevents](./hcpcsevents.md)
Billed events occurring during the hospitalization. Includes CPT codes.

#### [labevents](./labevents.md)
Laboratory measurements sourced from patient derived specimens.

#### [microbiologyevents](./microbiologyevents.md)
Microbiology cultures.

#### [patients](./patients.md) table
Patients' gender, age, and date of death if information exists.

#### [pharmacy](./pharmacy.md)
Formulary, dosing, and other information for prescribed medications.

#### [poe](./poe.md)
Orders made by providers relating to patient care.

#### [poe_detail](./poe_detail.md)
Supplementary information for orders made by providers in the hospital.

#### [prescriptions](./prescriptions.md)
Prescribed medications.

#### [procedures_icd](./procedures_icd.md)
Billed procedures for patients during their hospital stay.

#### [services](./services.md)
The hospital service(s) which cared for the patient during their hospitalization.

#### [transfers](./transfers.md) table
Detailed information about patients' unit transfers.
