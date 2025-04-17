---
title: "ICU stays"
linktitle: "icustays"
weight: 10
date: 2020-08-10
description: >
  Tracking information for ICU stays including admission and discharge times.
---

包括入院和出院时间的 ICU 停留跟踪信息。

# The icustays table

**Table source:** Hospital database.

**表来源:** 医院数据库。

**Table purpose:** Defines each ICU stay in the database using STAY\_ID.

**表用途:** 使用 STAY\_ID 定义数据库中的每个 ICU 停留。

**Number of rows:** 73,181

**行数:** 73,181

**Links to:**

* patients on `subject_id`
* admissions on `hadm_id`

**链接到:**

* `subject_id` 上的 patients 表
* `hadm_id` 上的 admissions 表

# Important considerations

* `stay_id` is a *generated* identifier that is *not* based on any raw data identifier. The hospital and ICU databases are not intrinsically linked and so do not have any concept of an ICU encounter identifier.

`stay_id` 是一个*生成*的标识符，*不*基于任何原始数据标识符。医院和 ICU 数据库没有内在联系，因此没有任何 ICU 遭遇标识符的概念。

* The `icustays` table is derived from the `transfers` table. Specifically, it excludes rows in `transfers` where the ward is not an ICU.

`icustays` 表是从 `transfers` 表派生的。具体来说，它排除了 `transfers` 表中病房不是 ICU 的行。

* Multiple consecutive icu stay entries from `transfers` are merged into a single entry in `transfers`.

来自 `transfers` 的多个连续 ICU 停留条目被合并为 `transfers` 中的单个条目。

* Heart rate measurements are used to determine if an icu stay is valid. If the heart rate measurement for an icu stay in `transfers` is not available, the icu stay will not be included in `icustays` (~5%).

心率测量用于确定 ICU 停留是否有效。如果 `transfers` 中 ICU 停留的心率测量不可用，ICU 停留将不包括在 `icustays` 中（约 5%）。

# Table columns

| Name            | Postgres data type |
|-----------------|--------------------|
| subject\_id     | INT                |
| hadm\_id        | INT                |
| stay\_id        | INT                |
| first\_careunit | VARCHAR(20)        |
| last\_careunit  | VARCHAR(20)        |
| intime          | TIMESTAMP(0)       |
| outtime         | TIMESTAMP(0)       |
| los             | DOUBLE PRECISION   |

# Detailed Description

## `subject_id`, `hadm_id`, `stay_id`

Identifiers which specify the patient: `subject_id` is unique to a patient, `hadm_id` is unique to a patient hospital stay and `stay_id` is unique to a patient ward stay.

指定患者的标识符：`subject_id` 对患者是唯一的，`hadm_id` 对患者的住院是唯一的，`stay_id` 对患者的病房停留是唯一的。

## `FIRST_CAREUNIT`, `LAST_CAREUNIT`

`FIRST_CAREUNIT` and `LAST_CAREUNIT` contain, respectively, the first and last ICU type in which the patient was cared for. As an `stay_id` groups all ICU admissions within 24 hours of each other, it is possible for a patient to be transferred from one type of ICU to another and have the same `stay_id`.

`FIRST_CAREUNIT` 和 `LAST_CAREUNIT` 分别包含患者接受护理的第一个和最后一个 ICU 类型。由于 `stay_id` 将所有 24 小时内的 ICU 入院分组，因此患者可能从一种 ICU 转移到另一种 ICU 并具有相同的 `stay_id`。

Care units are derived from the TRANSFERS table, and definition for the abbreviations can be found in the documentation for TRANSFERS.

护理单位是从 TRANSFERS 表派生的，缩写的定义可以在 TRANSFERS 的文档中找到。

## `INTIME`, `OUTTIME`

`INTIME` provides the date and time the patient was transferred into the ICU. `OUTTIME` provides the date and time the patient was transferred out of the ICU.

`INTIME` 提供了患者转入 ICU 的日期和时间。`OUTTIME` 提供了患者转出 ICU 的日期和时间。

## `LOS`

`LOS` is the length of stay for the patient for the given ICU stay, which may include one or more ICU units. The length of stay is measured in fractional days.

`LOS` 是患者在给定 ICU 停留期间的住院时间，可能包括一个或多个 ICU 单位。住院时间以小数天为单位测量。
