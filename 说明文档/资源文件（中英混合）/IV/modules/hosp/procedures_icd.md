---
title: "procedures_icd"
linktitle: "procedures_icd"
weight: 1
date: 2020-08-10
description: >
  Billed procedures for patients during their hospital stay.
---

## *procedures_icd*

During routine hospital care, patients are billed by the *hospital* for procedures they undergo.
This table contains a record of all procedures a patient was billed for during their hospital stay using the ICD-9 and ICD-10 ontologies.

在常规医院护理中，患者因接受的治疗程序而被医院收费。
此表记录了患者在住院期间使用 ICD-9 和 ICD-10 本体被收费的所有治疗程序。

### Links to

* *d_icd_procedures* on `icd_code` and `icd_version`

## Important considerations

- Procedures during the hospital stay can be billed (1) by the hospital or (2) by the provider. This table contains only procedures billed by the hospital.

在住院期间的治疗程序可以由（1）医院或（2）提供者收费。此表仅包含由医院收费的治疗程序。

## Table columns

| Name          | Postgres data type |
|---------------|--------------------|
| `subject_id`  | INTEGER NOT NULL   |
| `hadm_id`     | INTEGER NOT NULL   |
| `seq_num`     | INTEGER NOT NULL   |
| `chartdate`   | DATE NOT NULL      |
| `icd_code`    | VARCHAR(7)         |
| `icd_version` | INTEGER            |

### `subject_id`

{{% include "/static/include/subject_id.md" %}}

### `hadm_id`

{{% include "/static/include/hadm_id.md" %}}

## `seq_num`

An assigned priority for procedures which occurred within the hospital stay.

为住院期间发生的治疗程序分配的优先级。

## `chartdate`

The date of the associated procedures. Date does *not* strictly correlate with `seq_num`.

相关治疗程序的日期。日期与 `seq_num` 并不严格相关。

### `icd_code`, `icd_version`

`icd_code` is the International Coding Definitions (ICD) code.

`icd_code` 是国际编码定义 (ICD) 代码。

There are two versions for this coding system: version 9 (ICD-9) and version 10 (ICD-10). These can be differentiated using the `icd_version` column.
In general, ICD-10 codes are more detailed, though code mappings (or "cross-walks") exist which convert ICD-9 codes to ICD-10 codes.

此编码系统有两个版本：版本 9（ICD-9）和版本 10（ICD-10）。可以使用 `icd_version` 列来区分它们。
通常，ICD-10 代码更详细，尽管存在将 ICD-9 代码转换为 ICD-10 代码的代码映射（或“交叉引用”）。

Both ICD-9 and ICD-10 codes are often presented with a decimal. This decimal is not required for interpretation of an ICD code; i.e. the `icd_code` of '0010' is equivalent to '001.0'.

ICD-9 和 ICD-10 代码通常以小数形式表示。解释 ICD 代码时不需要这个小数；例如，`icd_code` 为 '0010' 等同于 '001.0'。
