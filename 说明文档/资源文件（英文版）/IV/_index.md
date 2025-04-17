**MIMIC-IV** is a relational database containing real hospital stays for patients admitted to a tertiary academic medical center in Boston, MA, USA. **MIMIC-IV** contains comprehensive information for each patient while they were in the hospital: laboratory measurements, medications administered, vital signs documented, and so on.
The database is intended to support a wide variety of research in healthcare.
MIMIC-IV builds upon the success of **MIMIC-III**, and incorporates numerous improvements over **MIMIC-III**.

MIMIC-IV is separated into "modules" to reflect the provenance of the data. There are currently five modules:

- [hosp](./modules/hosp/_index.md) - hospital level data for patients: labs, micro,  and  electronic medication administration
- [icu](./modules/icu/_index.md) - ICU level data. These are the event tables, and are identical in structure to MIMIC-III (chartevents, etc)
- [ed](./modules/ed/_index.md) - data from the emergency department
- [cxr](./modules/cxr/_index.md) - lookup tables and meta-data from MIMIC-CXR, allowing linking to MIMIC-IV
- [note](./modules/note/_index.md) - deidentified free-text clinical notes

---

MIMIC-Note is currently not publicly available and the structure is subject to change.

---

All patients across all datasets are in the [hosp](./modules/hosp) module. 

However, not all ICU patients have ED data, not all ICU patients have CXRs, not all ED patients have hospital data, and so on. Within an individual dataset, there are also incomplete tables as certain electronic systems did not exist in the past, particularly the eMAR system.


Tables for each module are detailed in the respective sections.
