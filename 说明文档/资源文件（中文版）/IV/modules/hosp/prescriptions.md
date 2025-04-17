---
title: "prescriptions"
linktitle: "prescriptions"
weight: 1
date: 2020-08-10
description: >
  Prescribed medications.
---

## *prescriptions*

The *prescriptions* table provides information about prescribed medications. Information includes the name of the drug, coded identifiers including the Generic Sequence Number (GSN) and National Drug Code (NDC), the product strength, the formulary dose, and the route of administration.

*prescriptions* 表提供了关于处方药物的信息。信息包括药物名称、编码标识符（包括通用序列号 (GSN) 和国家药物代码 (NDC)）、产品强度、处方剂量和给药途径。

## Links to

* *pharmacy* on `pharmacy_id`
* *emar* on `pharmacy_id`

<!--

# Important considerations

-->

## Table columns

| Name                | Postgres data type    |
|---------------------|-----------------------|
| `subject_id`        | INTEGER NOT NULL      |
| `hadm_id`           | INTEGER NOT NULL      |
| `pharmacy_id`       | INTEGER NOT NULL      |
| `poe_id`            | VARCHAR(25)           |
| `poe_seq`           | INTEGER               |
| `order_provider_id` | VARCHAR(10)           |
| `starttime`         | TIMESTAMP(3)          |
| `stoptime`          | TIMESTAMP(3)          |
| `drug_type`         | VARCHAR(20) NOT NULL  |
| `drug`              | VARCHAR(255) NOT NULL |
| `formulary_drug_cd` | VARCHAR(50)           |
| `gsn`               | VARCHAR(255)          |
| `ndc`               | VARCHAR(25)           |
| `prod_strength`     | VARCHAR(255)          |
| `form_rx`           | VARCHAR(25)           |
| `dose_val_rx`       | VARCHAR(100)          |
| `dose_unit_rx`      | VARCHAR(50)           |
| `form_val_disp`     | VARCHAR(50)           |
| `form_unit_disp`    | VARCHAR(50)           |
| `doses_per_24_hrs`  | REAL                  |
| `route`             | VARCHAR(50)           |

### `subject_id`

{{% include "/static/include/subject_id.md" %}}

### `hadm_id`

{{% include "/static/include/hadm_id.md" %}}

### `pharmacy_id`

An identifier which links administrations in *emar* to pharmacy information in the *pharmacy* table.

一个标识符，将 *emar* 中的管理与 *pharmacy* 表中的药房信息链接起来。

### `poe_id`, `poe_seq`

These columns allow linking prescriptions to associated orders in the *poe* table.

这些列允许将处方与 *poe* 表中的相关订单链接起来。

### `order_provider_id`

`order_provider_id` provides an anonymous identifier for the provider who initiated the order.
`order_provider_id` 为发起订单的提供者提供了一个匿名标识符。
{{% include "/static/include/provider_id.md" %}}

### `starttime`, `stoptime`

The prescribed start and stop time for the medication.

药物的处方开始和停止时间。

### `drug_type`

The component of the prescription which the drug occupies. Can be one of 'MAIN', 'BASE', or 'ADDITIVE'.

药物在处方中占据的组成部分。可以是 'MAIN'、'BASE' 或 'ADDITIVE' 之一。

### `drug`

A free-text description of the medication administered.

所给药物的自由文本描述。

### `formulary_drug_cd`

A hospital specific ontology used to order drugs from the formulary.

用于从处方中订购药物的医院特定本体。

### `gsn`

The Generic Sequence Number (GSN), a coded identifier used for medications.

通用序列号 (GSN)，用于药物的编码标识符。

### `ndc`

The National Drug Code (NDC), a coded identifier which uniquely identifiers medications.

国家药物代码 (NDC)，唯一标识药物的编码标识符。

### `prod_strength`

A free-text description of the composition of the prescribed medication (e.g. '12 mg / 0.8 mL Oral Syringe', '12.5mg Tablet', etc).

处方药物成分的自由文本描述（例如 '12 mg / 0.8 mL 口服注射器'、'12.5mg 片剂' 等）。

### `form_rx`

The container in which the formulary dose is delivered (e.g. 'TABLET', 'VIAL', etc).

处方剂量交付的容器（例如 '片剂'、'瓶装' 等）。

### `dose_val_rx`

The prescribed dose for the patient intended to be administered over the given time period.

在给定时间段内为患者开具的处方剂量。

### `dose_unit_rx`

The unit of measurement for the dose.

剂量的测量单位。

### `form_val_disp`

The amount of the medication which is contained in a single formulary dose.

单个处方剂量中包含的药物量。

### `form_unit_disp`

The unit of measurement used for the formulary dosage.

用于处方剂量的测量单位。

### `doses_per_24_hrs`

The number of doses per 24 hours for which the medication is to be given. A daily dose would result in `doses_per_24_hrs`: 1, bidaily (BID) would be 2, and so on.

每 24 小时给药的次数。每日剂量将导致 `doses_per_24_hrs` 为 1，每日两次 (BID) 将为 2，依此类推。

### `route`

The route of administration for the medication.

药物的给药途径。
