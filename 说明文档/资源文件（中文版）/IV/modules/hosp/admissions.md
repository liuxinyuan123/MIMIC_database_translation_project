---
title: "admissions table"
linktitle: "admissions"
date: 2020-08-10
weight: 1
description: >
  Detailed information about hospital stays.
---

The *admissions* table gives information regarding a patient's admission to the hospital. Since each unique hospital visit for a patient is assigned a unique `hadm_id`, the *admissions* table can be considered as a definition table for `hadm_id`. Information available includes timing information for admission and discharge, demographic information, the source of the admission, and so on.

*admissions* 表提供有关患者入院的信息。由于患者的每次唯一医院就诊都分配有一个唯一的`hadm_id`，因此 *入院* 表可以被视为 `hadm_id` 的定义表。可用信息包括入院和出院的时间信息、人口统计信息、入院来源等。

### 连接至

* *patients* on `subject_id`

## 重要注意事项

* The data is sourced from the admission, discharge and transfer database from the hospital (often referred to as 'ADT' data).
* Organ donor accounts are sometimes created for patients who died in the hospital. These are distinct hospital admissions with very short, sometimes negative lengths of stay. Furthermore, their `deathtime` is frequently the same as the earlier patient admission's `deathtime`.


* 数据来源于医院的入院、出院和转院数据库（通常称为“ADT”数据）。
* 器官捐献者账户有时会为在医院死亡的患者创建。这些是不同的住院患者，住院时间非常短，有时是负数。此外，他们的“死亡时间`deathtime`”通常与早期患者入院的“死亡时间`deathtime`”相同。

## Table columns

| Name                   | Postgres data type   |
|------------------------|----------------------|
| `subject_id`           | INTEGER NOT NULL     |
| `hadm_id`              | INTEGER NOT NULL     |
| `admittime`            | TIMESTAMP NOT NULL   |
| `dischtime`            | TIMESTAMP            |
| `deathtime`            | TIMESTAMP            |
| `admission_type`       | VARCHAR(40) NOT NULL |
| `admit_provider_id`    | VARCHAR(10)          |
| `admission_location`   | VARCHAR(60)          |
| `discharge_location`   | VARCHAR(60)          |
| `insurance`            | VARCHAR(255)         |
| `language`             | VARCHAR(10)          |
| `marital_status`       | VARCHAR(30)          |
| `race`                 | VARCHAR(80)          |
| `edregtime`            | TIMESTAMP            |
| `edouttime`            | TIMESTAMP            |
| `hospital_expire_flag` | SMALLINT             |

| 字段名                    | Postgres 数据类型        |
|------------------------|----------------------|
| `subject_id`           | INTEGER NOT NULL     |
| `hadm_id`              | INTEGER NOT NULL     |
| `admittime`            | TIMESTAMP NOT NULL   |
| `dischtime`            | TIMESTAMP            |
| `deathtime`            | TIMESTAMP            |
| `admission_type`       | VARCHAR(40) NOT NULL |
| `admit_provider_id`    | VARCHAR(10)          |
| `admission_location`   | VARCHAR(60)          |
| `discharge_location`   | VARCHAR(60)          |
| `insurance`            | VARCHAR(255)         |
| `language`             | VARCHAR(10)          |
| `marital_status`       | VARCHAR(30)          |
| `race`                 | VARCHAR(80)          |
| `edregtime`            | TIMESTAMP            |
| `edouttime`            | TIMESTAMP            |
| `hospital_expire_flag` | SMALLINT             |



## 详细描述

The *admissions* table defines all hospitalizations in the database. Hospitalizations are assigned a unique random integer known as the `hadm_id`.

*admissions* 表定义了数据库中的所有住院情况。住院人数被分配一个唯一的随机整数，称为`hadm_id`。

### `subject_id`, `hadm_id`

Each row of this table contains a unique `hadm_id`, which represents a single patient's admission to the hospital. `hadm_id` ranges from 2000000 - 2999999. It is possible for this table to have duplicate `subject_id`, indicating that a single patient had multiple admissions to the hospital. The ADMISSIONS table can be linked to the PATIENTS table using `subject_id`.

此表的每一行都包含一个唯一的 '`hadm_id`'，它表示单个患者的入院情况。'`hadm_id`' 的范围是 2000000 - 2999999。此表可能包含重复的 '`subject_id`'，表示单个患者多次入院。可以使用 '`subject_id`' 将 ADMISSIONS 表链接到 PATIENTS 表。

### `admittime`, `dischtime`, `deathtime`

`admittime` provides the date and time the patient was admitted to the hospital, while `dischtime` provides the date and time the patient was discharged from the hospital. If applicable, `deathtime` provides the time of in-hospital death for the patient. Note that `deathtime` is only present if the patient died in-hospital, and is almost always the same as the patient's `dischtime`. However, there can be some discrepancies due to typographical errors.

`admitTime`提供患者入院的日期和时间，而`dischTime`提供患者出院的日期和时间。如果适用，`deathtime
`提供患者在医院内死亡的时间。请注意，`deathtime`仅在患者在医院内死亡时出现，并且几乎总是与患者的`dischtime`相同。但是，由于拼写错误，可能会有一些差异。

### `admission_type`

`admission_type` is useful for classifying the urgency of the admission. There are 9 possibilities: 'AMBULATORY OBSERVATION', 'DIRECT EMER.', 'DIRECT OBSERVATION', 'ELECTIVE', 'EU OBSERVATION', 'EW EMER.', 'OBSERVATION ADMIT', 'SURGICAL SAME DAY ADMISSION', 'URGENT'.

`admission_type`可用于对 ADMISSION 的紧急性进行分类。有 9 种可能性： 'AMBULATORY OBSERVATION', 'DIRECT EMER.', 'DIRECT OBSERVATION', 'ELECTIVE', 'EU OBSERVATION', 'EW EMER.', 'OBSERVATION ADMIT', 'SURGICAL SAME DAY ADMISSION', 'URGENT'.

### `admit_provider_id`

`admit_provider_id` provides an anonymous identifier for the provider who admitted the patient.  
`admit_provider_id`  为收治患者的提供者提供匿名标识符。


### `admission_location`, `discharge_location`

`admission_location` provides information about the location of the patient prior to arriving at the hospital. Note that as the emergency room is technically a clinic, patients who are admitted via the emergency room usually have it as their admission location.

Similarly, `discharge_location` is the disposition of the patient after they are discharged from the hospital.

#### Association with UB-04 billing codes

`admission_location` and `discharge_location` are associated with internal hospital `ibax` codes which aren't provided in MIMIC-IV. These internal codes tend to align with UB-04 billing codes. 

In some cases more than one internal code is associated with a given `admission_location` and `discharge_location`. This can either be do to; 1) multiple codes being used by the hospital for the same `admission_location` or `discharge_location`, or 2) during de-identification multiple internal codes may be combined into a single `admission_location` or `discharge_location`. 

In the tables below, we provide the matching UB-04 code(s) for the most common `ibax` codes for a given `admission_location` and `discharge_location`, when applicable. In cases where more than one code is given, if this combination is due to 1) in the above paragraph, the additional code must have at least 10% of the entires of the most common code. 


**Admission UB-04 mappings:**

| admission_location                     | UB-04 code(s) |
|----------------------------------------|---------------|
| PHYSICIAN REFERRAL                     | 1, 3          | 
| WALK-IN/SELF REFERRAL                  | 1             |
| AMBULATORY SURGERY TRANSFER            | 1, 2, 6       |
| INFORMATION NOT AVAILABLE              | 1, 9          |
| CLINIC REFERRAL                        | 2, 8          |
| PROCEDURE SITE                         | 2             |
| PACU                                   | 2             |
| TRANSFER FROM HOSPITAL                 | 4, 6          |
| TRANSFER FROM SKILLED NURSING FACILITY | 5             |
| EMERGENCY ROOM                         | 1, 2, 7       |
| INTERNAL TRANSFER TO OR FROM PSYCH     | none          |


**Discharge UB-04 mappings:**

| discharge_location           | UB-04 code(s) |
|------------------------------|---------------|
| HOME                         | 01            |
| ACUTE HOSPITAL               | 02, 81, 86    |
| SKILLED NURSING FACILITY     | 03, 64        |
| ASSISTED LIVING              | 04            |
| HEALTHCARE FACILITY          | 05, 43        |
| HOME HEALTH CARE             | 06            |
| AGAINST ADVICE               | 07            |
| DIED                         | 20            |
| OTHER FACILITY               | 21, 70        |
| HOSPICE                      | 50, 51        |
| REHAB                        | 62            |
| CHRONIC/LONG TERM ACUTE CARE | 63            |
| PSYCH FACILITY               | 65            |
| OTHER FACILITY               | 70            |

UB-04 documentation online often provides more detail than found in the `admission_location` and `discharge_location` text, particularly for discharges.

在线 UB-04 文件通常提供比“`admission_location`”和“`discharge_location`”文本中更多的细节，特别是对于放电。

### `insurance`, `language`, `marital_status`, `ethnicity`

The `insurance`, `language`, `marital_status`, and `ethnicity` columns provide information about patient demographics for the given hospitalization.
Note that as this data is documented for each hospital admission, they may change from stay to stay.

`insurance`、`language`、`marital_status`和`ethnicity`列提供有关给定住院的患者人口统计信息。
请注意，由于每次入院都记录了这些数据，因此他们可能会因住院而异。

### `edregtime`, `edouttime`

The date and time at which the patient was registered and discharged from the emergency department.

患者登记和从急诊科出院的日期和时间。


### `hospital_expire_flag`

This is a binary flag which indicates whether the patient died within the given hospitalization. `1` indicates death in the hospital, and `0` indicates survival to hospital discharge.

这是一个二进制标志，指示患者是否在给定的住院治疗范围内死亡。“1”表示在医院死亡，“0”表示存活到出院。
