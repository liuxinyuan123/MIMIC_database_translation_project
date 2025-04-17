---
title: "transfers table"
linktitle: "transfers"
date: 2020-08-10
weight: 1
description: >
  Detailed information about patients' unit transfers. 
---

## *transfers*

Physical locations for patients throughout their hospital stay.

患者在住院期间的物理位置。

### Links to

* *patients* on `subject_id`
* *admissions* on `hadm_id`

## Important considerations

* The `icustays` table is derived from this table.

* `icustays` 表是从此表派生的。

## Table columns

| Name          | Postgres data type |
|---------------|--------------------|
| `subject_id`  | INTEGER NOT NULL   |
| `hadm_id`     | INTEGER            |
| `transfer_id` | INTEGER NOT NULL   |
| `eventtype`   | VARCHAR(10)        |
| `careunit`    | VARCHAR(255)       |
| `intime`      | TIMESTAMP(0)       |
| `outtime`     | TIMESTAMP(0)       |

## Detailed Description

## `subject_id`, `hadm_id`, `transfer_id`

Identifiers which specify the patient: `subject_id` is unique to a patient, `hadm_id` is unique to a patient hospital stay, and `transfer_id` is unique to a patient physical location.

指定患者的标识符：`subject_id` 对患者是唯一的，`hadm_id` 对患者的住院是唯一的，`transfer_id` 对患者的物理位置是唯一的。

Note that `stay_id` present in the *icustays* and *edstays* tables is derived from `transfer_id`. For example, three contiguous ICU stays will have three separate `transfer_id` for each distinct physical location (e.g. a patient could move from one bed to another). The entire stay will have a single `stay_id`, whih will be equal to the `transfer_id` of the first physical location.

请注意，*icustays* 和 *edstays* 表中的 `stay_id` 是从 `transfer_id` 派生的。例如，三个连续的 ICU 停留将为每个不同的物理位置（例如，患者可以从一张床移动到另一张床）拥有三个单独的 `transfer_id`。整个停留将拥有一个 `stay_id`，它将等于第一个物理位置的 `transfer_id`。

## `eventtype`

`eventtype` describes what transfer event occurred: 'ed' for an emergency department stay, 'admit' for an admission to the hospital, 'transfer' for an intra-hospital transfer and 'discharge' for a discharge from the hospital.

`eventtype` 描述了发生的转移事件：'ed' 表示急诊科停留，'admit' 表示入院，'transfer' 表示院内转移，'discharge' 表示出院。

## `careunit`

The type of unit or ward in which the patient is physically located. Examples of care units include medical ICUs, surgical ICUs, medical wards, new baby nurseries, and so on.

患者所在的单位或病房类型。护理单位的例子包括内科 ICU、外科 ICU、内科病房、新生儿护理室等。

## `intime`, `outtime`

`intime` provides the date and time the patient was transferred into the current care unit (`careunit`) from the previous care unit. `outtime` provides the date and time the patient was transferred out of the current physical location.

`intime` 提供了患者从上一个护理单位转移到当前护理单位 (`careunit`) 的日期和时间。`outtime` 提供了患者从当前物理位置转移出去的日期和时间。