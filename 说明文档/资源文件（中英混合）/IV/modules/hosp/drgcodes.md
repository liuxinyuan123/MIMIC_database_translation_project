---
title: "drgcodes"
linktitle: "drgcodes"
weight: 1
date: 2020-08-10
description: >
  Billed diagnosis related group (DRG) codes for hospitalizations.
---

## *drgcodes*

Diagnosis related groups (DRGs) are used by the hospital to obtain reimbursement for a patient's hospital stay.  

医院使用诊断相关组 (DRGs) 来为患者的住院治疗获得报销。

The codes correspond to the primary reason for a patient's stay at the hospital.  

这些代码对应于患者在医院停留的主要原因。

<!--

# Important considerations

-->

## Table columns

| Name            | Postgres data type |
|-----------------|--------------------|
| `subject_id`    | INTEGER            |
| `hadm_id`       | INTEGER            |
| `drg_type`      | VARCHAR(4)         |
| `drg_code`      | VARCHAR(10)        |
| `description`   | VARCHAR(195)       |
| `drg_severity`  | SMALLINT           |
| `drg_mortality` | SMALLINT           |

## Detailed Description

### `subject_id`

{{% include "/static/include/subject_id.md" %}}

### `hadm_id`

{{% include "/static/include/hadm_id.md" %}}

### `drg_type`

The specific DRG ontology used for the code.  

用于代码的特定 DRG 本体。

### `drg_code`

The DRG code.  
DRG 代码。

### `description`

A description for the given DRG code.  

给定 DRG 代码的描述。

### `drg_severity`, `drg_mortality`

Some DRG ontologies further qualify the patient severity of illness and likelihood of mortality, which are recorded here.  

某些 DRG 本体进一步量化了患者的病情严重程度和死亡可能性，这些信息在这里记录。
