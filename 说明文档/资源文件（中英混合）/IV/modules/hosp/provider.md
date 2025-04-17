---
title: "provider table"
linktitle: "provider"
date: 2023-02-03
weight: 1
description: >
  The provider table lists deidentified provider identifiers used in the database.
---

## *provider*

A description table for providers in the database referenced by *provider_id*.
As of MIMIC-IV v2.2, this table simply lists all unique `provider_id` in the database.

由 *provider_id* 引用的数据库中提供程序的描述表。
从 MIMIC-IV v2.2 开始，此表仅列出数据库中所有唯一的 `provider_id`。

Note that most tables contain a prefix before `provider_id`. All columns with a suffix link to `provider_id`, including:

请注意，大多数 table 在 'provider_id' 之前都包含前缀。带有后缀链接到 'provider_id' 的所有列，包括：

* `admit_provider_id`
* `enter_provider_id`
* `order_provider_id`

## 表列

| Name        | Postgres data type   |
|-------------|----------------------|
| provider_id | VARCHAR(10) NOT NULL |

### `provider_id`

`provider_id` lists all possible identifiers for providers used throughout the database.

`provider_id` 列出了整个数据库中使用的提供程序的所有可能标识符。

{{% include "/static/include/provider_id.md" %}}
