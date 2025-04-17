---
title: "outputevents"
linktitle: "outputevents"
weight: 10
date: 2020-08-10
description: >
  Information regarding patient outputs including urine, drainage, and so on.
---

关于患者输出的信息，包括尿液、引流等。

# The *outputevents* table

**Table source:** MetaVision ICU database.

**表来源:** MetaVision ICU 数据库。

**Table purpose:** Output data for patients.

**表用途:** 患者的输出数据。

**Number of rows:** 4,234,967

**行数:** 4,234,967

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

<!-- # Important considerations -->

# Table columns

| Name         | Data type        |
|--------------|------------------|
| subject\_id  | INTEGER          |
| hadm\_id     | INTEGER          |
| stay\_id     | INTEGER          |
| caregiver_id | INTEGER          |
| charttime    | TIMESTAMP(3)     |
| storetime    | TIMESTAMP(3)     |
| itemid       | INTEGER          |
| value        | DOUBLE PRECISION |
| valueuom     | VARCHAR(20)      |

# Detailed Description

## `subject_id`, `hadm_id`, `stay_id`

[//]: # (Identifiers which specify the patient: `subject_id` is unique to a patient, `hadm_id` is unique to a patient hospital stay and `stay_id` is unique to a patient ICU stay.)

指定患者的标识符：`subject_id` 对患者是唯一的，`hadm_id` 对患者的住院是唯一的，`stay_id` 对患者的 ICU 停留是唯一的。

### `caregiver_id`


## `charttime`

[//]: # (`charttime` is the time of an output event.)

`charttime` 是输出事件的时间。

## `storetime`

[//]: # (`storetime` records the time at which an observation was manually input or manually validated by a member of the clinical staff.)

`storetime` 记录了观察值被临床工作人员手动输入或手动验证的时间。

## `itemid`

[//]: # (Identifier for a single measurement type in the database. Each row associated with one `itemid` &#40;e.g. 212&#41; corresponds to an instantiation of the same measurement &#40;e.g. heart rate&#41;.)

数据库中单个测量类型的标识符。与一个 `itemid`（例如 212）关联的每一行对应于相同测量（例如心率）的一个实例。

## `value`, `valueuom`

[//]: # (`value` and `valueuom` list the amount of a substance at the `charttime` &#40;when the exact start time is unknown, but usually up to an hour before&#41;.)

`value` 和 `valueuom` 列出了在 `charttime` 时物质的量（当确切开始时间未知时，但通常在一小时之前）。
