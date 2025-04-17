---
title: "transfers table"
linktitle: "transfers"
date: 2020-08-10
weight: 1
description: >
  Detailed information about patients' unit transfers. 
---

## 转运

患者在住院期间的物理位置。

### Links to

* *patients* on `subject_id`
* *admissions* on `hadm_id`

## 重要信息

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

指定患者的标识符：`subject_id` 对患者是唯一的，`hadm_id` 对患者的住院是唯一的，`transfer_id` 对患者的物理位置是唯一的。

请注意，*icustays* 和 *edstays* 表中的 `stay_id` 是从 `transfer_id` 派生的。例如，三个连续的 ICU 停留将为每个不同的物理位置（例如，患者可以从一张床移动到另一张床）拥有三个单独的 `transfer_id`。整个停留将拥有一个 `stay_id`，它将等于第一个物理位置的 `transfer_id`。

## `eventtype`

`eventtype` 描述了发生的转移事件：'ed' 表示急诊科停留，'admit' 表示入院，'transfer' 表示院内转移，'discharge' 表示出院。

## `careunit`

患者所在的单位或病房类型。护理单位的例子包括内科 ICU、外科 ICU、内科病房、新生儿护理室等。

## `intime`, `outtime`


`intime` 提供了患者从上一个护理单位转移到当前护理单位 (`careunit`) 的日期和时间。`outtime` 提供了患者从当前物理位置转移出去的日期和时间。
