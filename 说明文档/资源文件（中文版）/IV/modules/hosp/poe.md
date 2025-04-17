---
title: "poe"
linktitle: "poe"
weight: 1
date: 2020-08-10
description: >
  Orders made by providers relating to patient care.
---

## *poe*

Provider order entry (POE) is the general interface through which care providers at the hospital enter orders. Most treatments and procedures must be ordered via POE.

提供者订单录入（POE）是医院护理提供者输入订单的通用界面。大多数治疗和程序必须通过 POE 进行订购。

## Links to

* *poe_detail* on `poe_id`

<!--

# Important considerations

-->

## Table columns

| Name                     | Postgres data type    |
|--------------------------|-----------------------|
| `poe_id`                 | VARCHAR(25) NOT NULL  |
| `poe_seq`                | INTEGER NOT NULL      |
| `subject_id`             | INTEGER NOT NULL      |
| `hadm_id`                | INTEGER               |
| `ordertime`              | TIMESTAMP(0) NOT NULL |
| `order_type`             | VARCHAR(25) NOT NULL  |
| `order_subtype`          | VARCHAR(50)           |
| `transaction_type`       | VARCHAR(15)           |
| `discontinue_of_poe_id`  | VARCHAR(25)           |
| `discontinued_by_poe_id` | VARCHAR(25)           |
| `order_provider_id`      | VARCHAR(10)           |
| `order_status`           | VARCHAR(15)           |

### `poe_id`

A unique identifier for the given order. `poe_id` is composed of `subject_id` and a monotonically increasing integer, `poe_seq`, in the following format: `subject_id`-`poe_seq`.

给定订单的唯一标识符。`poe_id` 由 `subject_id` 和一个单调递增的整数 `poe_seq` 组成，格式为：`subject_id`-`poe_seq`。

### `poe_seq`

A monotonically increasing integer which chronologically sorts the POE orders. That is, POE orders can be ordered sequentially by `poe_seq`.

一个单调递增的整数，按时间顺序对 POE 订单进行排序。也就是说，POE 订单可以按 `poe_seq` 顺序排列。

### `subject_id`

{{% include "/static/include/subject_id.md" %}}

### `hadm_id`

{{% include "/static/include/hadm_id.md" %}}

### `ordertime`

The date and time at which the provider order was made.

提供者订单的日期和时间。

### `order_type`

The type of provider order. One of the following:

提供者订单的类型。以下之一：

* ADT orders
* Blood Bank
* Cardiology
* Consults
* Critical Care
* General Care
* Hemodialysis
* IV therapy
* Lab
* Medications
* Neurology
* Nutrition
* OB
* Radiology
* Respiratory
* TPN

### `order_subtype`

Further detail on the type of order made by the provider. The `order_subtype` is best interpreted alongside the `order_type`, e.g. `order_type: 'Cardiology'` with `order_subtype: 'Holter Monitor'`.

提供者订单类型的进一步详细信息。`order_subtype` 最好与 `order_type` 一起解释，例如 `order_type: 'Cardiology'` 与 `order_subtype: 'Holter Monitor'`。

### `transaction_type`

The action which the provider performed when performing this order. One of the following:

提供者执行此订单时执行的操作。以下之一：

* Change
* Co
* D/C
* H
* New
* T

### `discontinue_of_poe_id`, `discontinued_by_poe_id`

If this order discontinues a previous order, then `discontinue_of_poe_id` will link to the previous order which was discontinued.
Conversely, if this order was later discontinued by a distinct order, then `discontinued_by_poe_id` will link to that future order.

如果此订单停用了先前的订单，则 `discontinue_of_poe_id` 将链接到被停用的先前订单。
相反，如果此订单后来被另一个订单停用，则 `discontinued_by_poe_id` 将链接到该未来订单。

### `order_provider_id`

`order_provider_id` provides an anonymous identifier for the provider who made the order.
`order_provider_id` 为下订单的提供者提供了一个匿名标识符。

{{% include "/static/include/provider_id.md" %}}

### `order_status`

Whether the order is still active ('Active') or whether it has been inactivated ('Inactive').

订单是否仍然活跃（'Active'）或是否已被停用（'Inactive'）。
