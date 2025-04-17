

## *prescriptions*



*prescriptions* 表提供了关于处方药物的信息。信息包括药物名称、编码标识符（包括通用序列号 (GSN) 和国家药物代码 (NDC)
）、用药强度、处方剂量和给药途径。

## 表连接

* *pharmacy* on `pharmacy_id`
* *emar* on `pharmacy_id`


## 表列

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
### `hadm_id`
### `pharmacy_id`

一个标识符，将 *emar* 中的管理与 *pharmacy* 表中的药房信息链接起来。

### `poe_id`, `poe_seq`

这些列允许将处方与 *poe* 表中的相关订单链接起来。

### `order_provider_id`

`order_provider_id` 为发起订单的提供者提供了一个匿名标识符。

### `starttime`, `stoptime`

药物的处方开始和停止时间。

### `drug_type`

药物在处方中占据的组成部分。可以是 'MAIN'、'BASE' 或 'ADDITIVE' 之一。

### `drug`

所给药物的自由文本描述。

### `formulary_drug_cd`

用于从处方中订购药物的医院特定本体。

### `gsn`

通用序列号 (GSN)，用于药物的编码标识符。

### `ndc`

国家药物代码 (NDC)，唯一标识药物的编码标识符。

### `prod_strength`

A free-text description of the composition of the prescribed medication (e.g. '12 mg / 0.8 mL Oral Syringe', '12.5mg Tablet', etc).

处方药物成分的自由文本描述（例如 '12 mg / 0.8 mL 口服注射器'、'12.5mg 片剂' 等）。

### `form_rx`

The container in which the formulary dose is delivered (e.g. 'TABLET', 'VIAL', etc).

处方剂量交付的容器（例如 '片剂'、'瓶装' 等）。

### `dose_val_rx`

在给定时间段内为患者开具的处方剂量。

### `dose_unit_rx`

剂量的测量单位。

### `form_val_disp`

单个处方剂量中包含的药物量。

### `form_unit_disp`

用于处方剂量的测量单位。

### `doses_per_24_hrs`

每 24 小时给药的次数。每日剂量将导致 `doses_per_24_hrs` 为 1，每日两次 (BID) 将为 2，依此类推。

### `route`
药物的给药途径。
