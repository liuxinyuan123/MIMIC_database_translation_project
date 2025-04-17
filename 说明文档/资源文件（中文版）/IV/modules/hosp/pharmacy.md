## *pharmacy*

药房表提供了关于患者开具的药物的详细信息。药房信息包括药物的剂量、处方剂量的数量、给药频率、给药途径和处方的持续时间。

## 表连接

* *poe* on `poe_id`
* *prescriptions* on `pharmacy_id`
* *emar* on `pharmacy_id`

## 表列描述

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

### `hadm_id`

### `pharmacy_id`

给定药房条目的唯一标识符。药房表的每一行都有一个唯一的 `pharmacy_id`。此标识符可用于将药房信息链接到提供者订单（在 *poe* 或 *prescriptions* 中）或药物的管理（在 *emar* 中）。

### `poe_id`

一个外键，链接到与此药房记录关联的 *prescriptions* 表中的提供者订单条目。

### `starttime`, `stoptime`

给定处方药物的开始和停止时间。

### `medication`
提供的药物名称。

### `proc_type`

类型："IV Piggyback"、"Non-formulary"、"Unit Dose" 等。

### `status`
处方是活跃的、不活跃的还是已停用的。

### `entertime`

处方进入药房系统的日期和时间。

### `verifiedtime`

处方被医生验证的日期和时间。

### `route`

处方的预期给药途径。

### `frequency`

药物应给患者给药的频率。频率列中使用了许多常用的缩写。Q# 表示每 # 小时；例如，"Q6" 或 "Q6H" 表示每 6 小时。

### `disp_sched`

药物应在一天中的哪些时间给药，例如 "08, 20" 表示药物应在上午 8:00 和晚上 8:00 分别给药。

### `infusion_type`

描述输液类型的编码字母：'B'、'C'、'N'、'N1'、'O' 或 'R'。

### `sliding_scale`

指示药物是否应按有浮动比例给药：'Y' 或 'N'。

### `lockout_interval`

患者必须等待的时间，直到他们自己提供另一剂药物；通常用于患者自控镇痛。

### `basal_rate`

药物在 24 小时内给药的速率。

### `one_hr_max`

在一小时内可以给予的最大剂量。

### `doses_per_24_hrs`


每 24 小时的预计给药次数。

**请注意：** 对于持续输注的药物，此列可能会产生误导，因为尽管是持续给药，但它们通常每天只“给药”一次。

### `duration`, `duration_interval`

`duration` 是给定剂量的用药时间的数字（无单位），而 `duration_interval` 可以被视为给定持续时间的测量单位。

> 例如，通常 
`duration` 为 1，`duration_interval` 为 "Doses"。或者，`duration` 可以是 8，`duration_interval` 可以是 "Weeks"。


### `expiration_value`, `expiration_unit`, `expirationdate`

如果药物有相关的停用日期，这些列详细说明了何时发生。`expiration_value` 和 `expiration_unit` 
提供了药物停用前的时间长度，例如 30 天、72 小时等。`expirationdate` 提供了去标识化的过期日期。

### `dispensation`
药物的分发来源。

### `fill_quantity`
要填充的处方比例。
