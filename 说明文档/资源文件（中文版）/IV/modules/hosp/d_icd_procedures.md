---
title: "d_icd_procedures"
linktitle: "d_icd_procedures"
weight: 1
date: 2020-08-10
description: >
  Dimension table for *procedures_icd*; provides a description of ICD-9/ICD-10 billed procedures.
  *procedures_icd* 的维度表;提供了 ICD-9/ICD-10 计费程序的描述。

---

## The *d_icd_procedures* table

This table defines International Classification of Diseases (ICD) codes for **procedures**. These codes are assigned at the end of the patient's stay and are used by the hospital to bill for care provided. They can further be used to identify if certain procedures have been performed (e.g. surgery).

下表定义了 **程序** 的国际疾病分类 （ICD） 代码。这些代码在患者住院结束时分配，并由医院用于为所提供的护理开具账单。它们可以进一步用于确定是否进行了某些程序（例如 手术）。


### 表连接

* *procedures_icd* on `icd_code` and `icd_version`

## 小结

<!-- # Important considerations -->

## 表列描述

| 字段            | Postgres 数据类型    |
|---------------|------------------|
| `icd_code`    | CHAR(7) NOT NULL |
| `icd_version` | INTEGER NOT NULL |
| `long_title`  | VARCHAR(255)     |

## 详细描述

### `icd_code`, `icd_version`

`icd_code` is the International Coding Definitions (ICD) code.

`icd_code` 是国际疾病分类 （ICD） 代码

There are two versions for this coding system: version 9 (ICD-9) and version 10 (ICD-10). These can be differentiated using the `icd_version` column. In general, ICD-10 codes are more detailed, though code mappings (or "cross-walks") exist which convert ICD-9 codes to ICD-10 codes.

此编码系统有两个版本：版本 9 （ICD-9） 和版本 10 （ICD-10）。这些可以使用 '`icd_version`' 列进行区分。一般来说，ICD-10 代码更详细，尽管存在将 ICD-9 代码转换为 ICD-10 代码的代码映射（或“cross-walks”）。

Both ICD-9 and ICD-10 codes are often presented with a decimal. This decimal is not required for interpretation of an ICD code; i.e. the `icd_code` of '0010' is equivalent to '001.0'.

ICD-9 和 ICD-10 代码通常都以小数表示。解释 ICD 代码时不需要这个小数;即 '0010' 的 '`icd_code`' 等同于 '001.0'。

## `long_title`

The title fields provide a brief definition for the given procedure code in `long_title`.

`long_title` 提供了给定程序代码的简要定义。
