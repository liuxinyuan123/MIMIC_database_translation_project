---
title: "chartevents"
linktitle: "chartevents"
weight: 10
date: 2020-08-10
description: >
  Charted items occurring during the ICU stay. Contains the majority of information documented in the ICU.

---

# The chartevents table

**Table source:** MetaVision ICU database.

**Table purpose:** Contains all charted data for all patients.

**Number of rows:** 313,645,063

**Links to:**

* patients on `subject_id`
* admissions on `hadm_id`
* icustays on `stay_id`
* d_items on `itemid`

# Brief summary

[//]: # (*chartevents* contains all the charted data available for a patient. During their ICU stay, the primary repository of a patient's information is their electronic chart. The electronic chart displays patients' routine vital signs and any additional information relevant to their care: ventilator settings, laboratory values, code status, mental status, and so on. As a result, the bulk of information about a patient's stay is contained in *chartevents*. Furthermore, even though laboratory values are captured elsewhere &#40;*labevents*&#41;, they are frequently repeated within *chartevents*. This occurs because it is desirable to display the laboratory values on the patient's electronic chart, and so the values are copied from the database storing laboratory values to the database storing the *chartevents*.)

*chartevents* 包含了患者的所有图表数据。在 ICU 停留期间，患者信息的主要存储库是他们的电子图表。电子图表显示患者的常规生命体征以及与其护理相关的任何其他信息：呼吸机设置、实验室值、代码状态、精神状态等。因此，关于患者停留的大部分信息都包含在 *chartevents* 中。此外，尽管实验室值在其他地方（*labevents*）被捕获，但它们经常在 *chartevents* 中重复。这是因为希望在患者的电子图表上显示实验室值，因此这些值从存储实验室值的数据库复制到存储 *chartevents* 的数据库中。

# Important considerations

[//]: # (* Some items are duplicated between the *labevents* and *chartevents* tables. In cases where there is disagreement between measurements, *labevents* should be taken as the ground truth.)

* 一些项目在 *labevents* 和 *chartevents* 表之间重复。在测量结果不一致的情况下，应以 *labevents* 为准。

# Table columns

| Name         | Postgres Data type |
|--------------|--------------------|
| subject\_id  | INTEGER            |
| hadm\_id     | INTEGER            |
| stay\_id     | INTEGER            |
| caregiver_id | INTEGER            |
| charttime    | TIMESTAMP(0)       |
| storetime    | TIMESTAMP(0)       |
| itemid       | INTEGER            |
| value        | VARCHAR(200)       |
| valuenum     | DOUBLE PRECISION   |
| valueuom     | VARCHAR(20)        |
| warning      | SMALLINT           |

## `subject_id`, `hadm_id`, `stay_id`

[//]: # (Identifiers which specify the patient: `subject_id` is unique to a patient, `hadm_id` is unique to a patient hospital stay and `stay_id` is unique to a patient ward stay. More information about these identifiers is [available here]&#40;/docs/iv/about/concepts/&#41;.)

指定患者的标识符：`subject_id` 对患者是唯一的，`hadm_id` 对患者的住院是唯一的，`stay_id` 对患者的病房停留是唯一的。有关这些标识符的更多信息[可在此处找到](/docs/iv/about/concepts/)。

### `caregiver_id`

## `charttime`, `storetime`

[//]: # ()
[//]: # (`charttime` records the time at which an observation was made, and is usually the closest proxy to the time the data was actually measured. `storetime` records the time at which an observation was manually input or manually validated by a member of the clinical staff.)

`charttime` 记录了观察值被记录的时间，通常是实际测量时间的最接近代理。`storetime` 记录了观察值被临床工作人员手动输入或手动验证的时间。

## `itemid`

[//]: # (Identifier for a single measurement type in the database. Each row associated with one `itemid` &#40;e.g. 220045&#41; corresponds to an instantiation of the same measurement &#40;e.g. heart rate&#41;.)

数据库中单个测量类型的标识符。与一个 `itemid`（例如 220045）关联的每一行对应于相同测量（例如心率）的一个实例。

## `value`, `valuenum`

[//]: # ()
[//]: # (`value` contains the value measured for the concept identified by the `itemid`. If this value is numeric, then `valuenum` contains the same data in a numeric format. If this data is not numeric, `valuenum` is null. In some cases &#40;e.g. scores like Glasgow Coma Scale, Richmond Sedation Agitation Scale and Code Status&#41;, `valuenum` contains the score and `value` contains the score and text describing the meaning of the score.)

`value` 包含为 `itemid` 标识的概念测量的值。如果此值是数字，则 `valuenum` 以数字格式包含相同的数据。如果此数据不是数字，则 `valuenum` 为 null。在某些情况下（例如格拉斯哥昏迷评分、里士满镇静躁动评分和代码状态），`valuenum` 包含评分，`value` 包含评分和描述评分含义的文本。

## `valueuom`

[//]: # (`valueuom` is the unit of measurement for the `value`, if appropriate.)

`valueuom` 是 `value` 的测量单位（如果适用）。

## `warning`

[//]: # ()
[//]: # (`warning` specifies if a warning for this observation was manually documented by the care provider.)

`warning` 指定是否由护理提供者手动记录了此观察值的警告。
