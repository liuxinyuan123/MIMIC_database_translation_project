---
title: "datetimeevents"
linktitle: "datetimeevents"
weight: 10
date: 2020-08-10
description: >
  Documented information which is in a date format (e.g. date of last dialysis).
---

记录为日期格式的信息（例如最后一次透析的日期）。

# The datetimeevents table

**Table source:** MetaVision ICU database.

**表来源:** MetaVision ICU 数据库。

**Table purpose:** Contains all date formatted data.

**表用途:** 包含所有日期格式的数据。

**Number of rows:** 7,112,999

**行数:** 7,112,999

**Links to:**

* patients on `subject_id`
* admissions on `hadm_id`
* icustays on `stay_id`
* d_items on `itemid`

**链接到:**

* `subject_id` 上的 patients 表
* `hadm_id` 上的 admissions 表
* `stay_id` 上的 icustays 表
* `itemid` 上的 d_items 表

# Table columns

| Name         | Postgres Data type |
|--------------|--------------------|
| subject\_id  | INTEGER            |
| hadm\_id     | INTEGER            |
| stay\_id     | INTEGER            |
| caregiver_id | INTEGER            |
| charttime    | TIMESTAMP(3)       |
| storetime    | TIMESTAMP(3)       |
| itemid       | INTEGER            |
| value        | TIMESTAMP(3)       |
| valueuom     | VARCHAR(20)        |
| warning      | SMALLINT           |

# Detailed Description

*datetimeevents* contains all date measurements about a patient in the ICU. For example, the date of last dialysis would be in the *datetimeevents* table, but the systolic blood pressure would not be in this table. As all dates in MIMIC are anonymized to protect patient confidentiality, all dates in this table have been shifted. Note that the chronology for an individual patient has been unaffected however, and quantities such as the difference between two dates remain true to reality.

*datetimeevents* 包含了 ICU 中患者的所有日期测量值。例如，最后一次透析的日期将出现在 *datetimeevents* 表中，但收缩压不会出现在此表中。由于 MIMIC 中的所有日期都已匿名化以保护患者隐私，因此此表中的所有日期都已进行了偏移。请注意，单个患者的时间顺序并未受到影响，两个日期之间的差异等数量仍然保持真实。

## `subject_id`, `hadm_id`, `stay_id`

Identifiers which specify the patient: `subject_id` is unique to a patient, `hadm_id` is unique to a patient hospital stay and `stay_id` is unique to a patient ward stay.

指定患者的标识符：`subject_id` 对患者是唯一的，`hadm_id` 对患者的住院是唯一的，`stay_id` 对患者的病房停留是唯一的。

### `caregiver_id`

{{% include "/static/include/caregiver_id.md" %}}

## `charttime`, `storetime`

`charttime` records the time at which an observation was charted, and is usually the closest proxy to the time the data was actually measured. `storetime` records the time at which an observation was manually input or manually validated by a member of the clinical staff.

`charttime` 记录了观察值被记录的时间，通常是实际测量时间的最接近代理。`storetime` 记录了观察值被临床工作人员手动输入或手动验证的时间。

## `itemid`

Identifier for a single measurement type in the database. Each row associated with one `itemid` (e.g. 212) corresponds to an instantiation of the same measurement (e.g. heart rate).

数据库中单个测量类型的标识符。与一个 `itemid`（例如 212）关联的每一行对应于相同测量（例如心率）的一个实例。

## `value`

The documented date - this is the value that corresponds to the concept referred to by `itemid`. For example, if querying for `itemid`: 225755 ("18 Gauge Insertion Date"), then the `value` column indicates the date the line was inserted.

记录的日期 - 这是与 `itemid` 所指概念对应的值。例如，如果查询 `itemid`: 225755（"18 Gauge Insertion Date"），则 `value` 列指示插入管线的日期。

## `valueuom`

The unit of measurement for the value - almost always the text string "Date".

值的测量单位 - 几乎总是文本字符串 "Date"。

## `warning`

`warning` specifies if a warning for this observation was manually documented by the care provider.

`warning` 指定是否由护理提供者手动记录了此观察值的警告。
