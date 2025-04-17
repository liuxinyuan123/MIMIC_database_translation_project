---
title: "d_icd_diagnoses"
linktitle: "d_icd_diagnoses"
weight: 1
date: 2020-08-10
description: >
  Dimension table for *diagnoses_icd*; provides a description of ICD-9/ICD-10 billed diagnoses.
  *diagnoses_icd* 的维度表;提供 ICD-9/ICD-10 计费诊断的描述。
---


## The *d_icd_diagnoses* table

This table defines International Classification of Diseases (ICD) Version 9 and 10 codes for **diagnoses**. These codes are assigned at the end of the patient's stay and are used by the hospital to bill for care provided.

此表定义了国际疾病分类 （ICD） 第 9 版和第 10 版的 **诊断** 代码。这些代码在患者住院结束时分配，并由医院用于为所提供的护理开具账单。

### 表连接

* *diagnoses_icd* ON `icd_code` and `icd_version`

<!-- # Important considerations -->

## 表列描述

| 名称            | Postgres 数据类型    |
|---------------|------------------|
| `icd_code`    | CHAR(7) NOT NULL |
| `icd_version` | INTEGER NOT NULL |
| `long_title`  | VARCHAR(255)     |

## 详细描述

### `icd_code`, `icd_version`

`icd_code` is the International Coding Definitions (ICD) code.

`icd_code` 国际疾病分类 （ICD）代码.

There are two versions for this coding system: version 9 (ICD-9) and version 10 (ICD-10). These can be differentiated using the `icd_version` column.

此编码系统有两个版本：版本 9 （ICD-9） 和版本 10 （ICD-10）。这些可以使用 `icd_version` 列进行区分。

In general, ICD-10 codes are more detailed, though code mappings (or "cross-walks") exist which convert ICD-9 codes to ICD-10 codes.

Both ICD-9 and ICD-10 codes are often presented with a decimal. This decimal is not required for interpretation of an ICD code; i.e. the `icd_code` of '0010' is equivalent to '001.0'.

ICD-9 和 ICD-10 代码通常都以小数表示。解释 ICD 代码时不需要这个小数;即 '0010' 的 `icd_code` 等同于 '001.0'。

ICD-9 and ICD-10 codes have distinct formats: ICD-9 codes are 5 character long strings which are entirely numeric (with the exception of codes prefixed with "E" or "V" which are used for external causes of injury or supplemental classification). Importantly, ICD-9 codes are retained as strings in the database as the leading 0s in codes are meaningful.

ICD-9 和 ICD-10 代码具有不同的格式：ICD-9 代码是 5 个字符长的字符串，完全是数字（前缀为“E”或“V”的代码除外，这些代码用于伤害的外部原因或补充分类）。重要的是，ICD-9 代码在数据库中保留为字符串，因为代码中的前导 0 有意义。

ICD-10 codes are 3-7 characters long and always prefixed by a letter followed by a set of numeric values.

ICD-10 代码是 3-7 个字符长，并且总是以字母开头，后跟一组数字。



### `long_title`

The `long_title` provides the meaning of the ICD code. For example, the ICD-9 code 0010 has `long_title` "Cholera due to vibrio cholerae".

`long_title`提供了 ICD 代码的含义。例如，ICD-9 代码 0010 有`long_title` “霍乱弧菌引起的霍乱”。
