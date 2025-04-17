

## *emar*


EMAR 表用于记录对单个患者进行的特定药物的给药。

该表中的记录由床边护理人员扫描与药物和患者相关的条形码填充。

## 表连接

* *emar_detail* on `emar_id`
* *pharmacy* on `pharmacy_id`
* *prescriptions* on `pharmacy_id`
* *poe* on `poe_id`


## Important considerations
* eMAR 系统在 2011-2013 年期间实施。因此，并非所有患者都有 eMAR 数据。

## 表列

| Name                | Postgres data type   |
|---------------------|----------------------|
| `subject_id`        | INTEGER NOT NULL     |
| `hadm_id`           | INTEGER              |
| `emar_id`           | VARCHAR(25) NOT NULL |
| `emar_seq`          | INTEGER NOT NULL     |
| `poe_id`            | VARCHAR(25) NOT NULL |
| `pharmacy_id`       | INTEGER              |
| `enter_provider_id` | VARCHAR(10)          |
| `charttime`         | TIMESTAMP NOT NULL   |
| `medication`        | TEXT                 |
| `event_txt`         | VARCHAR(100)         |
| `scheduletime`      | TIMESTAMP            |
| `storetime`         | TIMESTAMP NOT NULL   |

### `subject_id`

### `hadm_id`

### `emar_id`, `emar_seq`

eMAR 表的标识符。`emar_id` 是 eMAR 中每个订单的唯一标识符。`emar_seq` 是一个连续的整数，按时间顺序对 eMAR 订单进行编号。`emar_id` 由 `subject_id` 和 `emar_seq` 组成，模式如下：'`subject_id`-`emar_seq`'。

### `poe_id`

一个标识符，将 *emar* 中的给药与 *poe* 和 *prescriptions* 中的订单链接起来。

### `pharmacy_id`

一个标识符，将 *emar* 中的给药与 *pharmacy* 表中的药房信息链接起来。

### `enter_provider_id`

`enter_provider_id` 为将信息输入 eMAR 系统的提供者提供匿名标识符。


### `charttime`

药物给药的时间。

### `medication`

所给药物的名称。

### `event_txt`

有关给药的信息。最常见的 `event_txt` 是 'Administered'，但其他可能的值包括 'Applied'、'Confirmed'、'Delayed'、'Not Given' 等。

### `scheduletime`
如果存在，给药计划的时间。

### `storetime`
给药记录在 eMAR 表中的时间。
