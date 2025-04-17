---
title: "d_labitems"
linktitle: "d_labitems"
weight: 1
date: 2020-08-10
description: >
  Dimension table for *labevents* provides a description of all lab items.
---

## *d_labitems*

*d_labitems* contains definitions for all `itemid` associated with lab measurements in the MIMIC database. All data in *labevents* link to the *d_labitems* table. Each unique (`fluid`, `category`, `label`) tuple in the hospital database was assigned an `itemid` in this table, and the use of this `itemid` facilitates efficient storage and querying of the data.  
**实验室数据项表**

*d_labitems* 包含了 MIMIC 数据库中所有与实验室测量相关的 `itemid` 的定义。*labevents* 中的所有数据都链接到 *d_labitems* 表。医院数据库中每个唯一的 (`fluid`, `category`, `label`) 组合都被分配了一个 `itemid`，使用这个 `itemid` 可以高效地存储和查询数据。**

Laboratory data contains information collected and recorded in the hospital laboratory database. This includes measurements made in wards within the hospital and clinics outside the hospital. Most concepts in this table have been mapped to LOINC codes, an openly available ontology which facilitates interoperability.  
**实验室数据包含在医院实验室数据库中收集和记录的信息。这些信息包括医院内部病房和医院外部诊所的测量结果。此表中的大多数概念已被映射到 LOINC 代码，这是一种公开可用的本体，有助于实现互操作性。**

### Links to

* *labevents* on `itemid`  
**链接到**

* *labevents* 表的 `itemid`

## Important considerations

This table used to contain a column called `loinc_code`, which stored standardized identifiers for laboratory measurements. To support ongoing improvement of these labels, the assignment of LOINC codes is now done in the [MIMIC Code Repository](https://www.github.com/MIT-LCP/mimic-code).  
此表曾经包含一个名为 `loinc_code` 的列，用于存储实验室测量的标准标识符。为了支持这些标签的持续改进，LOINC 代码的分配现在在 [MIMIC Code Repository](https://www.github.com/MIT-LCP/mimic-code) 中完成。

## Table columns

| Name       | Postgres data type |
|------------|--------------------|
| `itemid`   | INTEGER            |
| `label`    | VARCHAR(50)        |
| `fluid`    | VARCHAR(50)        |
| `category` | VARCHAR(50)        |

**表列**

| 名称       | PostgreSQL 数据类型 |
|------------|--------------------|
| `itemid`   | INTEGER            |
| `label`    | VARCHAR(50)        |
| `fluid`    | VARCHAR(50)        |
| `category` | VARCHAR(50)        |

## Detailed Description

### `itemid`

A unique identifier for a laboratory concept. `itemid` is unique to each row, and can be used to identify data in labevents associated with a specific concept.  
实验室概念的唯一标识符。`itemid` 对每一行都是唯一的，可用于识别与特定概念相关的 *labevents* 中的数据。

### `label`

The `label` column describes the concept which is represented by the `itemid`.  
`label` 列描述了由 `itemid` 表示的概念。

### `fluid`

`fluid` describes the substance on which the measurement was made. For example, chemistry measurements are frequently performed on blood, which is listed in this column as 'BLOOD'. Many of these measurements are also acquirable on other fluids, such as urine, and this column differentiates these distinct concepts.  
`fluid` 描述了进行测量的物质。例如，化学测量通常在血液上进行，这在本列中被列为 'BLOOD'。这些测量中的许多也可以在其他流体（如尿液）上获得，本列区分了这些不同的概念。

### `category`

`category` provides higher level information as to the type of measurement. For example, a category of 'ABG' indicates that the measurement is an arterial blood gas.  
`category` 提供了更高层次的信息，说明了测量的类型。例如，类别为 'ABG' 表示该测量是动脉血气。