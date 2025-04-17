---
date: "2022-06-12T00:00:00-04:00"
title: "Ingredientevents"
linktitle: "Ingredientevents"
weight: 10
date: 2020-08-10
description: >
  Ingredients of continuous or intermittent administrations including nutritional and water content.
---

连续或间歇给药的成分，包括营养和水分含量。

# The *inputevents* table

**Table source:** MetaVision ICU database.

**表来源:** MetaVision ICU 数据库。

**Table purpose:** Ingredients contained within inputs data for patients.

**表用途:** 患者输入数据中包含的成分。

**Number of rows:** 12,229,408

**行数:** 12,229,408

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

* In the source data, there is no concept of a volume in the database: only a `rate`. All rows are recorded with a `starttime` and an `endtime`. The `amount` in this table is *derived* from the `rate` column, and provided for convenience. An exception is bolus administrations: these are listed as ending one minute after they started, i.e. `endtime`: `starttime` + 1 minute, and they do not have a `rate`.

在源数据中，数据库中没有体积的概念：只有 `rate`。所有行都记录有 `starttime` 和 `endtime`。此表中的 `amount` 是从 `rate` 列*推导*出来的，为了方便而提供。推注是一个例外：这些被列为开始后一分钟结束，即 `endtime`: `starttime` + 1 分钟，并且它们没有 `rate`。

# Table columns

| Name              | Postgres data type |
|-------------------|--------------------|
| subject\_id       | INTEGER            |
| hadm\_id          | INTEGER            |
| stay\_id          | INTEGER            |
| caregiver_id      | INTEGER            |
| starttime         | TIMESTAMP(0)       |
| endtime           | TIMESTAMP(0)       |
| storetime         | TIMESTAMP(0)       |
| itemid            | INTEGER            |
| amount            | DOUBLE PRECISION   |
| amountuom         | VARCHAR(20)        |
| rate              | DOUBLE PRECISION   |
| rateuom           | VARCHAR(20)        |
| orderid           | INTEGER            |
| linkorderid       | INTEGER            |
| statusdescription | VARCHAR(20)        |
| originalamount    | DOUBLE PRECISION   |
| originalrate      | DOUBLE PRECISION   |

# Detailed Description

## `subject_id`, `hadm_id`, `stay_id`

Identifiers which specify the patient: `subject_id` is unique to a patient, `hadm_id` is unique to a patient hospital stay and `stay_id` is unique to a patient ICU stay.

指定患者的标识符：`subject_id` 对患者是唯一的，`hadm_id` 对患者的住院是唯一的，`stay_id` 对患者的 ICU 停留是唯一的。

### `caregiver_id`

{{% include "/static/include/caregiver_id.md" %}}

## `starttime`, `endtime`

`starttime` and `endtime` record the start and end time of the event.

`starttime` 和 `endtime` 记录事件的开始和结束时间。

## `storetime`

`storetime` records the time at which an observation was manually input or manually validated by a member of the clinical staff.

`storetime` 记录了观察值被临床工作人员手动输入或手动验证的时间。

## `itemid`

Identifier for a single measurement type in the database. Each row associated with one `itemid` which corresponds to an instantiation of the same measurement (e.g. norepinephrine).

数据库中单个测量类型的标识符。与一个 `itemid` 关联的每一行对应于相同测量（例如去甲肾上腺素）的一个实例。

## `amount`, `amountuom`

`amount` and `amountuom` list the amount of a drug or substance administered to the patient either between the `starttime` and `endtime`.

`amount` 和 `amountuom` 列出了在 `starttime` 和 `endtime` 之间给患者施用的药物或物质的量。

## `rate`, `rateuom`

`rate` and `rateuom` list the rate at which the drug or substance was administered to the patient either between the `starttime` and `endtime`.

`rate` 和 `rateuom` 列出了在 `starttime` 和 `endtime` 之间给患者施用药物的速率。

## `orderid`, `linkorderid`

`orderid` links multiple items contained in the same solution together. For example, when a solution of noradrenaline and normal saline is administered both noradrenaline and normal saline occur on distinct rows but will have the same `orderid`.

`orderid` 将同一溶液中的多个项目链接在一起。例如，当去甲肾上腺素和生理盐水的溶液被施用时，去甲肾上腺素和生理盐水出现在不同的行中，但具有相同的 `orderid`。

`linkorderid` links the same order across multiple instantiations: for example, if the rate of delivery for the solution with noradrenaline and normal saline is changed, two new rows which share the same new `orderid` will be generated, but the `linkorderid` will be the same.

`linkorderid` 在多个实例中链接相同的订单：例如，如果去甲肾上腺素和生理盐水的溶液的输送速率改变，将生成两行新的数据，它们共享相同的新 `orderid`，但 `linkorderid` 将相同。

## `statusdescription`

`statusdescription` states the ultimate status of the item, or more specifically, row. It is used to indicate why the delivery of the compound has ended. There are only six possible statuses:

`statusdescription` 说明了项目的最终状态，或更具体地说，行的状态。它用于指示化合物输送结束的原因。只有六种可能的状态：

* Changed - The current delivery has ended as some aspect of it has changed (most frequently, the rate has been changed)
* Changed - 当前输送已结束，因为其某些方面已更改（最常见的是速率已更改）
* Paused - The current delivery has been paused
* Paused - 当前输送已暂停
* FinishedRunning - The delivery of the item has finished (most frequently, the bag containing the compound is empty)
* FinishedRunning - 项目的输送已完成（最常见的是包含化合物的袋子已空）
* Stopped - The delivery of the item been terminated by the caregiver
* Stopped - 项目的输送已被护理人员终止
* Rewritten - Incorrect information was input, and so the information in this row was rewritten (these rows are primarily useful for auditing purposes - the rates/amounts described were *not* delivered and so should not be used if determining what compounds a patient has received)
* Rewritten - 输入了错误的信息，因此此行中的信息被重写（这些行主要用于审计目的 - 描述的速率/量*未*被输送，因此在确定患者接受了哪些化合物时不应使用）
* Flushed - A line was flushed.
* Flushed - 管线已被冲洗。

## `originalamount`

Drugs are usually mixed within a solution and delivered continuously from the same bag. This column represents the amount of the compound contained in the bag at `starttime`.

药物通常混合在溶液中并从同一袋中连续输送。此列表示在 `starttime` 时袋中化合物的量。

## `originalrate`

This is the rate that was input by the care provider. Note that this may differ from `rate` because of various reasons: `originalrate` was the original planned rate, while the `rate` column will be the true rate delivered.

这是护理提供者输入的速率。请注意，由于各种原因，这可能与 `rate` 不同：`originalrate` 是原始计划速率，而 `rate` 列将是实际输送速率。
