[//]: # (---)

[//]: # (title: "d_items")

[//]: # (linktitle: "d_items")

[//]: # (weight: 1)

[//]: # (date: 2020-08-10)

[//]: # (description: >)

[//]: # (  Dimension table describing itemid. Defines concepts recorded in the events table in the ICU module.)

[//]: # (---)

描述 itemid 的维度表。定义了 ICU 模块中事件表中记录的概念。

# The d_items table

**Table source:** Metavision ICU databases.

**Table purpose:** Definition table for all items in the ICU databases.

**Number of rows:** 4,014

**Links to:**

* *chartevents* on `itemid`
* *datetimeevents* on `itemid`
* *inputevents* on `itemid`
* *outputevents* on `itemid`
* *procedureevents* on `itemid`

# Important considerations

[//]: # (* If the `linksto` column is null, then the data is currently unavailable, but planned for a future release.)

如果 `linksto` 列为空，则数据当前不可用，但计划在未来的版本中提供。

# Table columns

| Name            | Postgres data type |
|-----------------|--------------------|
| itemid          | INTEGER            |
| label           | VARCHAR(200)       |
| abbreviation    | VARCHAR(100)       |
| linksto         | VARCHAR(50)        |
| category        | VARCHAR(100)       |
| unitname        | VARCHAR(100)       |
| param\_type     | VARCHAR(30)        |
| lownormalvalue  | FLOAT              |
| highnormalvalue | FLOAT              |

# Detailed Description

[//]: # (The D_ITEMS table defines `itemid`, which represents measurements in the database. Measurements of the same type &#40;e.g. heart rate&#41; will have the same `itemid` &#40;e.g. 220045&#41;. Values in the `itemid` column are unique to each row. All `itemid`s will have a value > 220000.)

D_ITEMS 表定义了 `itemid`，它表示数据库中的测量值。相同类型的测量值（例如心率）将具有相同的 `itemid`（例如 220045）。`itemid` 列中的值对每一行都是唯一的。所有 `itemid` 的值都大于 220000。

## `itemid`

[//]: # ()
[//]: # (As an alternate primary key to the table, `itemid` is unique to each row.)

作为表的备用主键，`itemid` 对每一行都是唯一的。

## `label`, `abbreviation`

[//]: # ()
[//]: # (The `label` column describes the concept which is represented by the `itemid`. The `abbreviation` column, only available in Metavision, lists a common abbreviation for the label.)

`label` 列描述了由 `itemid` 表示的概念。`abbreviation` 列仅在 Metavision 中可用，列出了标签的常见缩写。

## `linksto`

[//]: # ()
[//]: # (`linksto` provides the table name which the data links to. For example, a value of 'chartevents' indicates that the `itemid` of the given row is contained in CHARTEVENTS. A single `itemid` is only used in one event table, that is, if an `itemid` is contained in CHARTEVENTS it will *not* be contained in any other event table &#40;e.g. IOEVENTS, CHARTEVENTS, etc&#41;.)

`linksto` 提供了数据链接到的表名。例如，'chartevents' 的值表示给定行的 `itemid` 包含在 CHARTEVENTS 中。单个 `itemid` 仅用于一个事件表，也就是说，如果 `itemid` 包含在 CHARTEVENTS 中，它将不会包含在任何其他事件表中（例如 IOEVENTS、CHARTEVENTS 等）。

## `category`

[//]: # (`category` provides some information of the type of data the `itemid` corresponds to. Examples include 'ABG', which indicates the measurement is sourced from an arterial blood gas, 'IV Medication', which indicates that the medication is administered through an intravenous line, and so on.)

`category` 提供了 `itemid` 对应的数据类型的一些信息。例如，'ABG' 表示测量值来自动脉血气，'IV Medication' 表示药物通过静脉注射给药，等等。

## `unitname`

[//]: # (`unitname` specifies the unit of measurement used for the `itemid`. This column is not always available, and this may be because the unit of measurement varies, a unit of measurement does not make sense for the given data type, or the unit of measurement is simply missing. Note that there is sometimes additional information on the unit of measurement in the associated event table, e.g. the `valueuom` column in CHARTEVENTS.)

`unitname` 指定了用于 `itemid` 的测量单位。此列并不总是可用，这可能是因为测量单位不同，测量单位对给定数据类型没有意义，或者测量单位缺失。请注意，在相关的事件表中有时会有关于测量单位的额外信息，例如 CHARTEVENTS 中的 `valueuom` 列。

## `param_type`

[//]: # ()
[//]: # (`param_type` describes the type of data which is recorded: a date, a number or a text field.)

`param_type` 描述了记录的数据类型：日期、数字或文本字段。

## `lownormalvalue`, `highnormalvalue`

[//]: # ()
[//]: # (These columns store reference ranges for the measurement. Note that a reference range encompasses the *expected* value of a measurement: values outside of this may still be physiologically plausible, but are considered unusual.)

这些列存储了测量的参考范围。请注意，参考范围涵盖了测量的预期值：超出此范围的值在生理上可能仍然是合理的，但被认为是异常的。
