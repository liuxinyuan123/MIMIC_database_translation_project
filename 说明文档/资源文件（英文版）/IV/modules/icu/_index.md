## ICU

----

The ICU module contains information collected from the clinical information system used within the ICU. Documented data includes intravenous administrations, ventilator settings, and other charted items.

The ICU module contains data sourced from the clinical information system at the BIDMC: MetaVision (iMDSoft). MetaVision tables were denormalized to create a star schema where the icustays and d_items tables link to a set of data tables all suffixed with “events”. 

Data documented in the icu module includes intravenous and fluid inputs (**inputevents**), ingredients of the aforementioned inputs (**ingredientevents**), patient outputs (**outputevents**), procedures (**procedureevents**), information documented as a date or time (**datetimeevents**), and other charted information (**chartevents**). All events tables contain a `stay_id` column allowing identification of the associated ICU patient in icustays, and an itemid column allowing identification of the concept documented in `d_items`.


### [caregiver](./caregiver.md) table
The [caregiver](./caregiver.md) table lists deidentified provider identifiers used in the ICU module.



### [d_items](./d_items.md)
Dimension table describing itemid. Defines concepts recorded in the events table in the ICU module.

### [chartevents](./chartevents.md)
Charted items occurring during the ICU stay. Contains the majority of information documented in the ICU.

### [datetimeevents](./datetimeevents.md)
Documented information which is in a date format (e.g. date of last dialysis).

### [icustays](./icustays.md)
Tracking information for ICU stays including admission and discharge times.

### [Ingredientevents](./ingredientevents.md)
Ingredients of continuous or intermittent administrations including nutritional and water content.

### [Inputevents](./inputevents.md)
Information documented regarding continuous infusions or intermittent administrations.

### [outputevents](./outputevents.md)
Information regarding patient outputs including urine, drainage, and so on.

### [procedureevents](./procedureevents.md)
Procedures documented during the ICU stay (e.g. ventilation), though not necessarily conducted within the ICU (e.g. x-ray imaging).
