---
title: "labevents"
linktitle: "labevents"
weight: 1
date: 2020-08-10
description: >
  Laboratory measurements sourced from patient derived specimens.
---

## *labevents*
实验室测量结果存储在 *labevents* 表中，涵盖了单个患者的所有实验室测量数据。

这些包括血液学测量、血气分析、化学面板以及较少见的测试，如遗传检测。

## 表连接

* *d_labitems* on `itemid`

## Important considerations

`hadm_id` 是通过 *transfers* 表分配给接近医院停留的实验室数据的。然而，这并不总是能完美捕捉到医院停留周围的实验室数据。

具体来说，截至 v2.1，可以使用 `subject_id`、`admittime` 和 `dischtime` 与 *admissions* 表连接，为 59,327,830 个观察值分配 `hadm_id`。然而，只有 58,131,956（98%）个观察值在 *labevents* 表中实际存储了 `hadm_id`。希望确保捕捉到接近医院停留的实验室数据的用户应意识到这一点，并根据需要使用时间连接。

以下条件必须满足，以便此数据在表中没有 `hadm_id`：


* 实验室观察必须不在 transfers 表的任何记录范围内
* 实验室观察必须没有关联的急诊停留标识符


SQL query for the above.


```
select 
  count(adm.hadm_id) as num_obs_in_hosp
  , count(le.subject_id) as num_obs_with_subject_id
  , count(le.hadm_id) as num_obs_with_hadm_id
  , count(le.hadm_id)*100.0/count(le.subject_id) as percent_obs_assigned_hadm_id
from hosp.admissions adm
left join hosp.labevents le
on adm.subject_id = le.subject_id
and le.charttime between adm.admittime and adm.dischtime;
```

## 表列描述

| Name                | Postgres data type |
|---------------------|--------------------|
| `labevent_id`       | INTEGER NOT NULL   |
| `subject_id`        | INTEGER NOT NULL   |
| `hadm_id`           | INTEGER            |
| `specimen_id`       | INTEGER NOT NULL   |
| `itemid`            | INTEGER NOT NULL   |
| `order_provider_id` | VARCHAR(10)        |
| `charttime`         | TIMESTAMP(0)       |
| `storetime`         | TIMESTAMP(0)       |
| `value`             | VARCHAR(200)       |
| `valuenum`          | DOUBLE PRECISION   |
| `valueuom`          | VARCHAR(20)        |
| `ref_range_lower`   | DOUBLE PRECISION   |
| `ref_range_upper`   | DOUBLE PRECISION   |
| `flag`              | VARCHAR(10)        |
| `priority`          | VARCHAR(7)         |
| `comments`          | TEXT               |

### `labevent_id`

一个整数，对于表中的每一行都是唯一的。

### `subject_id`

### `hadm_id`

### `specimen_id`

唯一地表示了进行实验室测量的标本。大多数实验室测量都是基于患者衍生样本（标本）进行的，例如血液、尿液等。

通常会在同一标本上进行多次测量。`specimen_id` 将对同一标本上的测量结果进行分组，例如从同一血液样本中进行的血气测量。

### `itemid`

一个唯一标识实验室概念的标识符。

### `order_provider_id`

`order_provider_id` 为使用实验室测量的提供者提供了一个匿名标识符。

### `charttime`


实验室测量被记录的时间。这通常是获取标本的时间，通常比测量结果可用的时间早得多。

### `storetime`
测量结果在实验室系统中可用的时间。此时信息将对护理提供者可用。

### `value`, `valuenum`
实验室测量的结果，如果是数值，则将其转换为数值数据类型。

### `valueuom`
实验室概念的单位。

### `ref_range_lower`, `ref_range_upper`
参考范围的上限和下限，表示实验室测量的正常范围。超出参考范围的值被认为是异常的。

### `flag`
一个简短的字符串，主要用于指示实验室测量是否异常。

### `priority`

The priority of the laboratory measurement: either routine or stat (urgent).

实验室测量的优先级：常规或紧急。

### `comments`
与实验室测量相关的去标识化自由文本注释。通常这些提供有关样本的信息，是否已向护理提供者告知了结果，解释考虑因素，或者在某些情况下，注释包含实验室本身的结果。已完全去标识化的注释（即没有保留任何信息内容）以三个下划线表示：`___`。`NULL` 注释表示该行没有注释。
