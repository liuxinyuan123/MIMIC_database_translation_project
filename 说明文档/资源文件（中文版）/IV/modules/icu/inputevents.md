---
date: "2015-09-01T19:34:46-04:00"
title: "Inputevents"
linktitle: "inputevents"
weight: 10
date: 2020-08-10
description: >
  Information documented regarding continuous infusions or intermittent administrations.
---

关于连续输注或间歇给药的信息记录。

# The *inputevents* table

**Table source:** MetaVision ICU database.

**表来源:** MetaVision ICU 数据库。

**Table purpose:** Input data for patients.

**表用途:** 患者的输入数据。

**Number of rows:** 8,978,893

**行数:** 8,978,893

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

# Brief example

The original source database recorded input data using two tables: RANGESIGNALS and ORDERENTRY. These tables do not appear in MIMIC as they have been merged to form the INPUTEVENTS table. RANGESIGNALS contains recorded data elements which last for a fixed period of time. Furthermore, the RANGESIGNALS table recorded information for each component of the drug separately. For example, for a norepinephrine administration there would be two components: a main order component (norepinephrine) and a solution component (NaCl). The `starttime` and `endtime` of RANGESIGNALS indicated when the drug started and finished. *Any* change in the drug rate would result in the current infusion ending, and a new `starttime` being created.

原始源数据库使用两个表记录输入数据：RANGESIGNALS 和 ORDERENTRY。这些表在 MIMIC 中不出现，因为它们已被合并形成 INPUTEVENTS 表。RANGESIGNALS 包含持续固定时间段的记录数据元素。此外，RANGESIGNALS 表分别记录了药物的每个成分的信息。例如，对于去甲肾上腺素的给药，会有两个成分：主要订单成分（去甲肾上腺素）和溶液成分（NaCl）。RANGESIGNALS 的 `starttime` 和 `endtime` 指示药物开始和结束的时间。*任何*药物速率的变化都会导致当前输注结束，并创建一个新的 `starttime`。

Let's examine an example of a patient being given norepinephrine.

让我们来看一个患者接受去甲肾上腺素给药的例子。

| Item           | `starttime` | `endtime` | `rate` | `rateuom`  | `orderid` | `linkorderid` |
|----------------|-------------|-----------|--------|------------|-----------|---------------|
| Norepinephrine | 18:20       | 18:25     | 1      | mcg/kg/min | 8003      | 8003          |
| NaCl           | 18:20       | 18:25     | 10     | ml/hr      | 8003      | 8003          |
| Norepinephrine | 18:25       | 20:00     | 2      | mcg/kg/min | 8020      | 8003          |
| NaCl           | 18:25       | 20:00     | 20     | ml/hr      | 8020      | 8003          |

The `starttime` for the solution (NaCl) and the drug (norepinephrine) would be 18:20. The rate of the drug is 1 mcg/kg/min, and the rate of the solution is 10 mL/hr. The nurse decides to increase the drug rate at 18:25 to 2 mcg/kg/min. As a result, the `endtime` for the two rows corresponding to the solution (NaCl and norepinephrine) is set to 18:25. Two new rows are generated with a `starttime` of 18:25. These two new rows would continue until either (i) the drug rate was changed or (ii) the drug was delivery was discontinued. The `orderid` column is used to group drug delivery with rate of delivery. In this case, we have NaCl and norepinephrine in the same bag delivered at the same time - as a result their `orderid` is the same (8003). When the rate is changed, a new `orderid` is generated (8020). The column `linkorderid` can be used to link this drug across all administrations, even when the rate is changed. Note also that `linkorderid` is always equal to the first `orderid` which occurs for the solution, as demonstrated in the example above.

溶液（NaCl）和药物（去甲肾上腺素）的 `starttime` 为 18:20。药物的速率为 1 mcg/kg/min，溶液的速率为 10 mL/hr。护士决定在 18:25 将药物速率增加到 2 mcg/kg/min。因此，溶液（NaCl 和去甲肾上腺素）对应的两行的 `endtime` 被设置为 18:25。生成两行新的数据，`starttime` 为 18:25。这两行新数据将持续到（i）药物速率改变或（ii）药物输送停止。`orderid` 列用于将药物输送与输送速率分组。在这种情况下，NaCl 和去甲肾上腺素在同一袋中同时输送，因此它们的 `orderid` 相同（8003）。当速率改变时，会生成一个新的 `orderid`（8020）。`linkorderid` 列可用于在所有给药中链接该药物，即使速率改变。请注意，`linkorderid` 始终等于溶液的第一个 `orderid`，如上例所示。

# Important considerations

* For Metavision data, there is no concept of a volume in the database: only a `rate`. All inputs are recorded with a `starttime` and an `endtime`. As a result, the volumes in the database for Metavision patients are *derived* from the rates. Furthermore, exact start and stop times for the drugs are easily deducible.

对于 Metavision 数据，数据库中没有体积的概念：只有 `rate`。所有输入都记录有 `starttime` 和 `endtime`。因此，Metavision 患者的数据库中的体积是从速率*推导*出来的。此外，药物的确切开始和停止时间很容易推导出来。

* A bolus will be listed as ending one minute after it started, i.e. `endtime`: `starttime` + 1 minute

推注将被列为开始后一分钟结束，即 `endtime`: `starttime` + 1 分钟。

# Table columns

| Name                          | Postgres data type |
|-------------------------------|--------------------|
| subject\_id                   | INT                |
| hadm\_id                      | INT                |
| stay\_id                      | INT                |
| caregiver_id                  | INTEGER            |
| starttime                     | TIMESTAMP(0)       |
| endtime                       | TIMESTAMP(0)       |
| storetime                     | TIMESTAMP(0)       |
| itemid                        | INT                |
| amount                        | DOUBLE PRECISION   |
| amountuom                     | VARCHAR(30)        |
| rate                          | DOUBLE PRECISION   |
| rateuom                       | VARCHAR(30)        |
| orderid                       | BIGINT             |
| linkorderid                   | BIGINT             |
| ordercategoryname             | VARCHAR(100)        |
| secondaryordercategoryname    | VARCHAR(100)        |
| ordercomponenttypedescription | VARCHAR(200)        |
| ordercategorydescription      | VARCHAR(50)        |
| patientweight                 | DOUBLE PRECISION   |
| totalamount                   | DOUBLE PRECISION   |
| totalamountuom                | VARCHAR(50)        |
| `isopenbag`                   | SMALLINT           |
| statusdescription             | VARCHAR(30)        |
| originalamount                | DOUBLE PRECISION   |
| originalrate                  | DOUBLE PRECISION   |

# Detailed Description

## `subject_id`, `hadm_id`, `stay_id`

Identifiers which specify the patient: `subject_id` is unique to a patient, `hadm_id` is unique to a patient hospital stay and `stay_id` is unique to a patient ICU stay.

指定患者的标识符：`subject_id` 对患者是唯一的，`hadm_id` 对患者的住院是唯一的，`stay_id` 对患者的 ICU 停留是唯一的。

### `caregiver_id`

{{% include "/static/include/caregiver_id.md" %}}

## `starttime`, `endtime`

`starttime` and `endtime` record the start and end time of an input/output event.

`starttime` 和 `endtime` 记录输入/输出事件的开始和结束时间。

## `storetime`

`storetime` records the time at which an observation was manually input or manually validated by a member of the clinical staff.

`storetime` 记录了观察值被临床工作人员手动输入或手动验证的时间。

## `itemid`

Identifier for a single measurement type in the database. Each row associated with one `itemid` which corresponds to an instantiation of the same measurement (e.g. norepinephrine).

数据库中单个测量类型的标识符。与一个 `itemid` 关联的每一行对应于相同测量（例如去甲肾上腺素）的一个实例。

## `amount`, `amountuom`

`amount` and `amountuom` list the amount of a drug or substance administered to the patient either between the `starttime` and `endtime`.

`amount` 和 `amountuom` 列出了在 `starttime` 和 `endtime` 之间给患者施用的药物或物质的量。

## rate, rateuom

`rate` and `rateuom` list the rate at which the drug or substance was administered to the patient either between the `starttime` and the `endtime`.

`rate` 和 `rateuom` 列出了在 `starttime` 和 `endtime` 之间给患者施用药物的速率。

## orderid, linkorderid

`orderid` links multiple items contained in the same solution together. For example, when a solution of noradrenaline and normal saline is administered both noradrenaline and normal saline occur on distinct rows but will have the same `orderid`.

`orderid` 将同一溶液中的多个项目链接在一起。例如，当去甲肾上腺素和生理盐水的溶液被施用时，去甲肾上腺素和生理盐水出现在不同的行中，但具有相同的 `orderid`。

`linkorderid` links the same order across multiple instantiations: for example, if the rate of delivery for the solution with noradrenaline and normal saline is changed, two new rows which share the same new `orderid` will be generated, but the `linkorderid` will be the same.

`linkorderid` 在多个实例中链接相同的订单：例如，如果去甲肾上腺素和生理盐水的溶液的输送速率改变，将生成两行新的数据，它们共享相同的新 `orderid`，但 `linkorderid` 将相同。

## `ordercategoryname`, `secondaryordercategoryname`, `ordercomponenttypedescription`, `ordercategorydescription`

These columns provide higher level information about the order the medication/solution is a part of. Categories represent the type of administration, while the `ordercomponenttypedescription` describes the role of the substance in the solution (i.e. main order parameter, additive, or mixed solution)

这些列提供了关于药物/溶液所属订单的更高层次信息。类别表示给药类型，而 `ordercomponenttypedescription` 描述了物质在溶液中的作用（即主要订单参数、添加剂或混合溶液）。

## `patientweight`

The patient weight in kilograms.

患者的体重，单位为千克。

## `totalamount`, `totalamountuom`

Intravenous administrations are usually given by hanging a bag of fluid at the bedside for continuous infusion over a certain period of time. These columns list the total amount of the fluid in the bag containing the solution.

静脉注射通常通过在床边悬挂一袋液体进行持续输注。这些列列出了包含溶液的袋中液体的总量。

## `isopenbag`

Whether the order was from an open bag.

订单是否来自打开的袋子。

## `continueinnextdept`

If the order ended on patient transfer, this field indicates if it continued into the next department (e.g. a floor).

如果订单在患者转移时结束，此字段指示它是否继续到下一个部门（例如普通病房）。

## `statusdescription`

`statusdescription` states the ultimate status of the item, or more specifically, row. It is used to indicate why the delivery of the compound has ended. There are only six possible statuses:

`statusdescription` 说明了项目的最终状态，或更具体地说，行的状态。它用于指示化合物输送结束的原因。只有六种可能的状态：

* Changed - The current delivery has ended as some aspect of it has changed (most frequently, the rate has been changed)
* Paused - The current delivery has been paused
* FinishedRunning - The delivery of the item has finished (most frequently, the bag containing the compound is empty)
* Stopped - The delivery of the item been terminated by the caregiver
* Flushed - A line was flushed.

* Changed - 当前输送已结束，因为其某些方面已更改（最常见的是速率已更改）
* Paused - 当前输送已暂停
* FinishedRunning - 项目的输送已完成（最常见的是包含化合物的袋子已空）
* Stopped - 项目的输送已被护理人员终止
* Flushed - 管线已被冲洗。

## `originalamount`

Drugs are usually mixed within a solution and delivered continuously from the same bag. This column represents the amount of the drug contained in the bag at `starttime`. For the first infusion of a new bag, `originalamount`: `totalamount`. Later on, if the rate is changed, then the amount of the drug in the bag will be lower (as some has been administered to the patient). As a result, `originalamount` < `totalamount`, and `originalamount` will be the amount of drug leftover in the bag at that `starttime`.

药物通常混合在溶液中并从同一袋中连续输送。此列表示在 `starttime` 时袋中药物的量。对于新袋的第一次输注，`originalamount`: `totalamount`。之后，如果速率改变，袋中药物的量将减少（因为一些药物已施用于患者）。因此，`originalamount` < `totalamount`，`originalamount` 将是该 `starttime` 时袋中剩余的药量。

## `originalrate`

This is the rate that was input by the care provider. Note that this may differ from `rate` because of various reasons: `originalrate` was the original planned rate, while the `rate` column will be the true rate delivered. For example, if a a bag is about to run out and the care giver decides to push the rest of the fluid, then `rate` > `originalrate`.
However, these two columns are usually the same, but have minor non-clinically significant differences due to rounding error.

这是护理提供者输入的速率。请注意，由于各种原因，这可能与 `rate` 不同：`originalrate` 是原始计划速率，而 `rate` 列将是实际输送速率。例如，如果袋子即将用完，护理人员决定推动剩余的液体，则 `rate` > `originalrate`。
然而，这两列通常是相同的，但由于舍入误差，存在微小的非临床显著差异。
