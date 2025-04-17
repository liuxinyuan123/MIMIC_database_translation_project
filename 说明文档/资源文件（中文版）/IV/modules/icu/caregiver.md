[//]: # (---)

[//]: # (title: "caregiver table")

[//]: # (linktitle: "caregiver")

[//]: # (date: 2023-02-03)

[//]: # (weight: 1)

[//]: # (description: >)

[//]: # (  The caregiver table lists deidentified provider identifiers used in the ICU module.)

[//]: # (---)

[//]: # ()
[//]: # (## *caregiver*)

[//]: # ()
[//]: # (A description table for the ICU caregivers in the ICU module referenced by *caregiver_id*.)

[//]: # (As of MIMIC-IV v2.2, this table simply lists all unique `caregiver_id` in the database.)

[//]: # ()
[//]: # (Note that, in order to distinguish identifiers used in the hospital wide EHR from those used in the ICU information system, we have adopted the nomenclature of "caregivers" for the ICU &#40;`caregiver_id` and *caregivers*&#41;. For the hospital data in the hosp module, we use the terminology of "providers" &#40;`provider_id` and *providers*&#41;. However, conceptually, both these sets of identifiers and tables refer to practicing providers at the hospital.)

[//]: # ()
[//]: # (## Table columns)

[//]: # ()
[//]: # (| Name         | Postgres data type   |)

[//]: # (|--------------|----------------------|)

[//]: # (| caregiver_id | VARCHAR&#40;10&#41; NOT NULL |)

[//]: # ()
[//]: # (### `caregiver_id`)

[//]: # ()
[//]: # (`caregiver_id` lists all possible identifiers for caregivers used in the ICU module.)

[//]: # (---)

[//]: # ()
[//]: # (title: "caregiver 表")

[//]: # (linktitle: "caregiver")

[//]: # (date: 2023-02-03)

[//]: # (weight: 1)

[//]: # (description: >)

[//]: # (  caregiver 表列出了 ICU 模块中使用的去标识化提供者标识符。)

[//]: # (---)

## *caregiver*

ICU 模块中 ICU 护理人员的描述表，由 *caregiver_id* 引用。
截至 MIMIC-IV v2.2，此表仅列出数据库中所有唯一的 `caregiver_id`。

请注意，为了区分医院范围内的 EHR 中使用的标识符与 ICU 信息系统中使用的标识符，我们采用了“caregivers”这一术语用于 ICU（`caregiver_id` 和 *caregivers*）。对于 hosp 模块中的医院数据，我们使用“providers”这一术语（`provider_id` 和 *providers*）。然而，从概念上讲，这两组标识符和表都指的是医院中的执业提供者。

## 表列

| 名称           | Postgres 数据类型        |
|--------------|----------------------|
| caregiver_id | VARCHAR(10) NOT NULL |

### `caregiver_id`

`caregiver_id` 列出了 ICU 模块中使用的所有可能的护理人员标识符。
