---
title: "pharmacy"
linktitle: "pharmacy"
weight: 1
date: 2020-08-10
description: >
  Formulary, dosing, and other information for prescribed medications.
---

## *pharmacy*

The pharmacy table provides detailed information regarding filled medications which were prescribed to the patient.
Pharmacy information includes the dose of the drug, the number of formulary doses, the frequency of dosing, the medication route, and the duration of the prescription.

药房表提供了关于患者开具的药物的详细信息。药房信息包括药物的剂量、处方剂量的数量、给药频率、给药途径和处方的持续时间。

## Links to

* *poe* on `poe_id`
* *prescriptions* on `pharmacy_id`
* *emar* on `pharmacy_id`

## Table columns

| Name                | Postgres data type    |
|---------------------|-----------------------|
| `subject_id`        | INTEGER NOT NULL      |
| `hadm_id`           | INTEGER NOT NULL      |
| `pharmacy_id`       | INTEGER NOT NULL      |
| `poe_id`            | VARCHAR(25)           |
| `starttime`         | TIMESTAMP(3)          |
| `stoptime`          | TIMESTAMP(3)          |
| `medication`        | TEXT                  |
| `proc_type`         | VARCHAR(50) NOT NULL  |
| `status`            | VARCHAR(50)           |
| `entertime`         | TIMESTAMP(3) NOT NULL |
| `verifiedtime`      | TIMESTAMP(3)          |
| `route`             | VARCHAR(50)           |
| `frequency`         | VARCHAR(50)           |
| `disp_sched`        | VARCHAR(255)          |
| `infusion_type`     | VARCHAR(15)           |
| `sliding_scale`     | VARCHAR(1)            |
| `lockout_interval`  | VARCHAR(50)           |
| `basal_rate`        | REAL                  |
| `one_hr_max`        | VARCHAR(10)           |
| `doses_per_24_hrs`  | REAL                  |
| `duration`          | REAL                  |
| `duration_interval` | VARCHAR(50)           |
| `expiration_value`  | INTEGER               |
| `expiration_unit`   | VARCHAR(50)           |
| `expirationdate`    | TIMESTAMP(3)          |
| `dispensation`      | VARCHAR(50)           |
| `fill_quantity`     | VARCHAR(50)           |

### `subject_id`

{{% include "/static/include/subject_id.md" %}}

### `hadm_id`

{{% include "/static/include/hadm_id.md" %}}

### `pharmacy_id`

A unique identifier for the given pharmacy entry.
Each row of the pharmacy table has a unique `pharmacy_id`. This identifier can be used to link the pharmacy information to the provider order (in *poe* or *prescriptions*) or to the administration of the medication (in *emar*).

给定药房条目的唯一标识符。药房表的每一行都有一个唯一的 `pharmacy_id`。此标识符可用于将药房信息链接到提供者订单（在 *poe* 或 *prescriptions* 中）或药物的管理（在 *emar* 中）。

### `poe_id`

A foreign key which links to the provider order entry order in the *prescriptions* table associated with this pharmacy record.

一个外键，链接到与此药房记录关联的 *prescriptions* 表中的提供者订单条目。

### `starttime`, `stoptime`

The start and stop times for the given prescribed medication.

给定处方药物的开始和停止时间。

### `medication`

The name of the medication provided.

提供的药物名称。

### `proc_type`

The type of order: "IV Piggyback", "Non-formulary", "Unit Dose", and so on.

订单类型："IV Piggyback"、"Non-formulary"、"Unit Dose" 等。

### `status`

Whether the prescription is active, inactive, or discontinued.

处方是活跃的、不活跃的还是已停用的。

### `entertime`

The date and time at which the prescription was entered into the pharmacy system.

处方进入药房系统的日期和时间。

### `verifiedtime`

The date and time at which the prescription was verified by a physician.

处方被医生验证的日期和时间。

### `route`

The intended route of administration for the prescription.

处方的预期给药途径。

### `frequency`

The frequency at which the medication should be administered to the patient. Many commonly used short hands are used in the frequency column.
Q# indicates every # hours; e.g. "Q6" or "Q6H" is every 6 hours.

药物应给患者给药的频率。频率列中使用了许多常用的缩写。Q# 表示每 # 小时；例如，"Q6" 或 "Q6H" 表示每 6 小时。

### `disp_sched`

The hours of the day at which the medication should be administered, e.g. "08, 20" would indicate the medication should be administered at 8:00 AM and 8:00 PM, respectively.

药物应在一天中的哪些时间给药，例如 "08, 20" 表示药物应在上午 8:00 和晚上 8:00 分别给药。

### `infusion_type`

A coded letter describing the type of infusion: 'B', 'C', 'N', 'N1', 'O', or 'R'.

描述输液类型的编码字母：'B'、'C'、'N'、'N1'、'O' 或 'R'。

### `sliding_scale`

Indicates whether the medication should be given on a sliding scale: either 'Y' or 'N'.

指示药物是否应按滑动比例给药：'Y' 或 'N'。

### `lockout_interval`

The time the patient must wait until providing themselves with another dose; often used with patient controlled analgesia.

患者必须等待的时间，直到他们自己提供另一剂药物；通常用于患者自控镇痛。

### `basal_rate`

The rate at which the medication is given over 24 hours.

药物在 24 小时内给药的速率。

### `one_hr_max`

The maximum dose that may be given in a single hour.

在一小时内可以给予的最大剂量。

### `doses_per_24_hrs`

The number of expected doses per 24 hours. Note that this column can be misleading for continuously infused medications as they are usually only "dosed" once per day, despite continuous administration.

每 24 小时的预期剂量数。请注意，对于持续输注的药物，此列可能会产生误导，因为尽管是持续给药，但它们通常每天只“给药”一次。

### `duration`, `duration_interval`

`duration` is the numeric duration of the given dose, while `duration_interval` can be considered as the unit of measurement for the given duration. For example, often `duration` is 1 and `duration_interval` is "Doses". Alternatively, `duration` could be 8 and the `duration_interval` could be "Weeks".

`duration` 是给定剂量的数字持续时间，而 `duration_interval` 可以被视为给定持续时间的测量单位。例如，通常 `duration` 为 1，`duration_interval` 为 "Doses"。或者，`duration` 可以是 8，`duration_interval` 可以是 "Weeks"。

### `expiration_value`, `expiration_unit`, `expirationdate`

If the drug has a relevant expiry date, these columns detail when this occurs. `expiration_value` and `expiration_unit` provide a length of time until the drug expires, e.g. 30 days, 72 hours, and so on. `expirationdate` provides the deidentified date of expiry.

如果药物有相关的过期日期，这些列详细说明了何时发生。`expiration_value` 和 `expiration_unit` 提供了药物过期前的时间长度，例如 30 天、72 小时等。`expirationdate` 提供了去标识化的过期日期。

### `dispensation`

The source of dispensation for the medication.

药物的分发来源。

### `fill_quantity`

What proportion of the formulary to fill.

要填充的处方比例。
