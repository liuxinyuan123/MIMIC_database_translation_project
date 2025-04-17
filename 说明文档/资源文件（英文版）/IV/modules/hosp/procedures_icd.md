---
title: "procedures_icd"
linktitle: "procedures_icd"
weight: 1
date: 2020-08-10
description: >
  Billed procedures for patients during their hospital stay.
---

## *procedures_icd*

During routine hospital care, patients are billed by the *hospital* for procedures they undergo.
This table contains a record of all procedures a patient was billed for during their hospital stay using the ICD-9 and ICD-10 ontologies.

### Links to

* *d_icd_procedures* on `icd_code` and `icd_version`

## Important considerations

- Procedures during the hospital stay can be billed (1) by the hospital or (2) by the provider. This table contains only procedures billed by the hospital.

## Table columns

Name | Postgres data type
---- | ----
`subject_id` | INTEGER NOT NULL
`hadm_id` | INTEGER NOT NULL
`seq_num` | INTEGER NOT NULL
`chartdate` | DATE NOT NULL
`icd_code` | VARCHAR(7)
`icd_version` | INTEGER

### `subject_id`

{{% include "/static/include/subject_id.md" %}}

### `hadm_id`

{{% include "/static/include/hadm_id.md" %}}

## `seq_num`

An assigned priority for procedures which occurred within the hospital stay.

## `chartdate`

The date of the associated procedures. Date does *not* strictly correlate with `seq_num`.

### `icd_code`, `icd_version`

`icd_code` is the International Coding Definitions (ICD) code.

There are two versions for this coding system: version 9 (ICD-9) and version 10 (ICD-10). These can be differentiated using the `icd_version` column.
In general, ICD-10 codes are more detailed, though code mappings (or "cross-walks") exist which convert ICD-9 codes to ICD-10 codes.

Both ICD-9 and ICD-10 codes are often presented with a decimal. This decimal is not required for interpretation of an ICD code; i.e. the `icd_code` of '0010' is equivalent to '001.0'.
