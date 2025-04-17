---
title: "procedureevents"
linktitle: "procedureevents"
weight: 10
date: 2020-08-10
description: >
  Procedures documented during the ICU stay (e.g. ventilation), though not necessarily conducted within the ICU (e.g. x-ray imaging).
---

在 ICU 停留期间记录的程序（例如通气），尽管不一定在 ICU 内进行（例如 X 射线成像）。

# The procedureevents table

**Table source:** MetaVision ICU database.

**表来源:** MetaVision ICU 数据库。

**Table purpose:** Contains procedures for patients

**表用途:** 包含患者的医嘱。

**Number of rows:** 696,092

**行数:** 696,092

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

# Important considerations

[//]: # (This table is **not** a required documentation field during routine care. As a result, existence of procedures here indicates their presence, but absence does not indicate the procedure was not conducted. The consistency of documentation varies by the type of procedure. For example, invasive ventilation tends to be documented, whereas non-invasive documentation is less consistently documented.)

此表**不是**常规护理中的必填文档字段。因此，此处存在程序表明其存在，但不存在并不表示未进行该程序。文档的一致性因程序类型而异。例如，有创通气往往会被记录，而无创记录的文档一致性较低。

# Table columns

| Name                     | Data type        |
|--------------------------|------------------|
| subject\_id              | INTEGER          |
| hadm\_id                 | INTEGER          |
| stay\_id                 | INTEGER          |
| caregiver_id             | INTEGER          |
| starttime                | TIMESTAMP        |
| endtime                  | TIMESTAMP        |
| storetime                | TIMESTAMP        |
| itemid                   | INTEGER          |
| value                    | DOUBLE PRECISION |
| valueuom                 | VARCHAR(20)      |
| location                 | VARCHAR(100)     |
| locationcategory         | VARCHAR(50)      |
| orderid                  | INTEGER          |
| linkorderid              | INTEGER          |
| ordercategoryname        | VARCHAR(50)      |
| ordercategorydescription | VARCHAR(30)      |
| patientweight            | DOUBLE PRECISION |
| isopenbag                | SMALLINT         |
| continueinnextdept       | SMALLINT         |
| statusdescription        | VARCHAR(20)      |
| originalamount           | DOUBLE PRECISION |
| originalrate             | DOUBLE PRECISION |

# Detailed Description

## `subject_id`, `hadm_id`, `stay_id`

[//]: # (Identifiers which specify the patient: `subject_id` is unique to a patient, `hadm_id` is unique to a patient hospital stay and `stay_id` is unique to a patient ICU stay.)

指定患者的标识符：`subject_id` 对患者是唯一的，`hadm_id` 对患者的住院是唯一的，`stay_id` 对患者的 ICU 停留是唯一的。

### `caregiver_id`
## `starttime`, `endtime`

[//]: # (`starttime` and `endtime` record the start and end time of an event.)

`starttime` 和 `endtime` 记录事件的开始和结束时间。

## `storetime`

[//]: # (`storetime` specifies the time when the event was recorded in the system.)

`storetime` 指定事件在系统中记录的时间。

## `itemid`

[//]: # (Identifier for a single measurement type in the database. Each row associated with one `itemid` &#40;e.g. 212&#41; corresponds to a type of measurement &#40;e.g. heart rate&#41;. The *d_items* table may be joined on this field. For any itemid appearing in the *procedureevents* table, *d_items* `linksto` column will have the value 'procedureevents'.)

数据库中单个测量类型的标识符。与一个 `itemid`（例如 212）关联的每一行对应于一种测量类型（例如心率）。*d_items* 表可以在此字段上进行连接。对于出现在 *procedureevents* 表中的任何 itemid，*d_items* 表的 `linksto` 列将具有值 'procedureevents'。

## `value`

[//]: # (In the `procedureevents` table, this identifies the duration of the procedure &#40;if applicable&#41;. For example, if querying for itemid 225794 &#40;“Non-invasive Ventilation”&#41;, then the value column indicates the duration of ventilation therapy.)

在 `procedureevents` 表中，这标识了程序的持续时间（如果适用）。例如，如果查询 itemid 225794（“无创通气”），则 value 列指示通气治疗的持续时间。

## `valueuom`

[//]: # (The unit of measurement for the value. Most frequently "None" &#40;no value recorded&#41;; otherwise one of "day", "hour", or "min". A query for itemiid 225794 &#40;"Non-invasive Ventilation"&#41; returning a `value` of 461 and `valueuom` of 'min' would correspond to non-invasive ventilation provided for 461 minutes; this value is expected to match the difference between the `starttime` and `endtime` fields for the record. A procedure with `valueuom` equal to "None" corresponds to a procedure which is instantaneous &#40;e.g. intubation, patient transfer&#41; or whose duration is not relevant &#40;e.g. imaging procedures&#41;. For these records, there will be a difference of one second between `starttime` and `endtime` values.)

值的测量单位。最常见的是“None”（未记录值）；否则为“day”、“hour”或“min”之一。查询 itemiid 225794（“无创通气”）返回 `value` 为 461 且 `valueuom` 为 'min' 将对应于提供 461 分钟的无创通气；此值应与记录的 `starttime` 和 `endtime` 字段之间的差异相匹配。`valueuom` 等于“None”的程序对应于瞬时程序（例如插管、患者转移）或其持续时间不相关的程序（例如成像程序）。对于这些记录，`starttime` 和 `endtime` 值之间将有一秒的差异。

## `location` , `locationcategory`

[//]: # (`location` and `locationcategory` provide information about where on the patient's body the procedure is taking place. For example, the `location` might be 'Left Upper Arm' and the `locationcategory` might be 'Invasive Venous'.)

`location` 和 `locationcategory` 提供有关程序在患者身体上发生位置的信息。例如，`location` 可能是“左上臂”，而 `locationcategory` 可能是“有创静脉”。

## `orderid`, `linkorderid`

[//]: # (These columns link procedures to specific physician orders. Unlike in the `mimic_icu.inputevents` table, most procedures in `procedureevents` are ordered independently.)

这些列将程序链接到特定的医生订单。与 `mimic_icu.inputevents` 表不同，`procedureevents` 中的大多数程序是独立下医嘱的。

[//]: # (There are a limited number of records for which the same procedure was performed again at a later date under the same original order. When a procedure was repeated under the same original order, the `linkorderid` field of the record for the later procedure will be set to the `orderid` field of the earlier record. In all other cases, `orderid` = `linkorderid`.)

有少量记录是在同一原始订单下在稍后日期再次执行相同程序。当在同一原始订单下重复程序时，后期程序的记录的 `linkorderid` 字段将设置为早期记录的 `orderid` 字段。在所有其他情况下，`orderid` = `linkorderid`。

## `ordercategoryname`, `ordercategorydescription`

[//]: # (These columns provide higher level information about the medication/solution order. Categories represent the type of administration.)

这些列提供了有关药物/溶液订单的更高层次信息。类别表示给药类型。

## `patientweight`

The patient weight in kilograms.

患者的体重，单位为千克。

## `isopenbag`

Whether the order was from an open bag.

订单是否来自打开的袋子。

## `continueinnextdept`

If the order ended on patient transfer, this field indicates if it continued into the next department (e.g. a floor).

如果订单在患者转移时结束，此字段指示它是否继续到下一个部门（例如普通病房）。

## `statusdescription`

[//]: # (`statusdescription` states the ultimate status of the procedure referred to in the row. The statuses appearing on the `procedureevents` table are:)

`statusdescription` 说明了行中提到的程序的最终状态。出现在 `procedureevents` 表中的状态有：

[//]: # (* `Paused` - The current delivery has been paused.)
* `Paused` - 当前输送已暂停。

[//]: # (* `FinishedRunning` - The delivery of the item has finished &#40;most frequently, the bag containing the compound is empty&#41;.)
* `FinishedRunning` - 项目的输送已完成（最常见的是包含化合物的袋子已空）。

[//]: # (* `Stopped` - The delivery of the item been terminated by the caregiver.)
* `Stopped` - 项目的输送已被护理人员终止。

Nearly all procedures recorded in *procedureevents* have a status of `FinishedRunning`.

几乎所有记录在 *procedureevents* 中的程序的状态都是 `FinishedRunning`。

## `originalamount`, `originalrate`

[//]: # (These fields are present in the table and never null, but have no clear meaning.)

[//]: # (In particular, "originalrate" is either 0 or 1 for all records.)

这些字段存在于表中且从不为空，但没有明确的含义。
特别是，“`originalrate`”对于所有记录要么为 0，要么为 1。
