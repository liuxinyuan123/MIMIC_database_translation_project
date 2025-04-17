## *poe*

提供者订单录入Provider order entry （POE）是医院护理提供者输入医嘱的通用界面。大多数治疗和程序必须通过 POE 进行下医嘱。

## 表连接

* *poe_detail* on `poe_id`


## 表列描述

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

给定医嘱的唯一标识符。`poe_id` 由 `subject_id` 和一个单调递增的整数 `poe_seq` 
组成，格式为：`subject_id`-`poe_seq`。

### `poe_seq`

一个单调递增的整数，按时间顺序对 POE 医嘱进行排序。也就是说，POE 医嘱可以按 `poe_seq` 顺序排列。

### `subject_id`
### `hadm_id`
### `ordertime`

提供者医嘱的日期和时间。

### `order_type`

提供者医嘱的类型。以下之一：

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

提供者医嘱类型的进一步详细信息。`order_subtype` 最好与 `order_type` 一起解释，例如 `order_type: 
'Cardiology'` 与 `order_subtype: 'Holter Monitor'`。

### `transaction_type`

提供者执行此医嘱时执行的操作。以下之一：

* Change
* Co
* D/C
* H
* New
* T

### `discontinue_of_poe_id`, `discontinued_by_poe_id`


如果此医嘱停用了先前的医嘱，则 `discontinue_of_poe_id` 将链接到被停用的先前医嘱。
相反，如果此医嘱后来被另一个医嘱停用，则 `discontinued_by_poe_id` 将链接到该未来医嘱。

### `order_provider_id`

`order_provider_id` 为下医嘱的提供者提供了一个匿名标识符。


### `order_status`
医嘱是否仍然活跃（'Active'）或是否已被停用（'Inactive'）。
