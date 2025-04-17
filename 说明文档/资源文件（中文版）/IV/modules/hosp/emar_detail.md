## *emar_detail*

*emar_detail* 表包含在 EMAR 表中进行的每次药物给药的信息。


信息包括相关的药房订单、应给药剂量、实际给药剂量以及与医疗管理相关的许多其他参数。

## 表连接

* *emar* on `emar_id`
* *pharmacy* on `pharmacy_id`

## Important considerations


* eMAR 系统在 2011-2013 年期间实施。因此，并非所有患者都有 eMAR 数据。

## 表列

| Name                                   | Postgres data type   |
|----------------------------------------|----------------------|
| `subject_id`                           | INTEGER NOT NULL     |
| `emar_id`                              | VARCHAR(25) NOT NULL |
| `emar_seq`                             | INTEGER NOT NULL     |
| `parent_field_ordinal`                 | VARCHAR(10)          |
| `administration_type`                  | VARCHAR(50)          |
| `pharmacy_id`                          | INTEGER              |
| `barcode_type`                         | VARCHAR(4)           |
| `reason_for_no_barcode`                | TEXT                 |
| `complete_dose_not_given`              | VARCHAR(5)           |
| `dose_due`                             | VARCHAR(100)         |
| `dose_due_unit`                        | VARCHAR(50)          |
| `dose_given`                           | VARCHAR(255)         |
| `dose_given_unit`                      | VARCHAR(50)          |
| `will_remainder_of_dose_be_given`      | VARCHAR(5)           |
| `product_amount_given`                 | VARCHAR(30)          |
| `product_unit`                         | VARCHAR(30)          |
| `product_code`                         | VARCHAR(30)          |
| `product_description`                  | VARCHAR(255)         |
| `product_description_other`            | VARCHAR(255)         |
| `prior_infusion_rate`                  | VARCHAR(40)          |
| `infusion_rate`                        | VARCHAR(40)          |
| `infusion_rate_adjustment`             | VARCHAR(50)          |
| `infusion_rate_adjustment_amount`      | VARCHAR(30)          |
| `infusion_rate_unit`                   | VARCHAR(30)          |
| `route`                                | VARCHAR(10)          |
| `infusion_complete`                    | VARCHAR(1)           |
| `completion_interval`                  | VARCHAR(50)          |
| `new_iv_bag_hung`                      | VARCHAR(1)           |
| `continued_infusion_in_other_location` | VARCHAR(1)           |
| `restart_interval`                     | TEXT                 |
| `side`                                 | VARCHAR(10)          |
| `site`                                 | VARCHAR(255)         |
| `non_formulary_visual_verification`    | VARCHAR(1)           |

### `subject_id`

### `emar_id`, `emar_seq`


eMAR 表的标识符。`emar_id` 是 eMAR 中每个订单的唯一标识符。`emar_seq` 是一个连续的整数，按时间顺序对 eMAR 订单进行编号。`emar_id` 由 `subject_id` 和 `emar_seq` 组成，模式如下：'`subject_id`-`emar_seq`'。

### `parent_field_ordinal`

`parent_field_ordinal` 描述了同一 eMar 事件的多次给药，例如完整剂量的多个配方剂量。由于 eMAR 要求管理提供者为提供给患者的每个配方扫描条形码，因此通常 *emar_detail* 中的多行对应于 *emar* 的单行（例如，多次给药以达到所需剂量）。*emar_detail* 行的结构如下：


* 每个 eMAR 订单有一行 `parent_field_ordinal` 为 NULL：此行通常包含给药的所需剂量。


* 之后，如果有 N 个配方剂量，`parent_field_ordinal` 将取值 '1.1', '1.2', ..., '1.N'。


最常见的情况是每种药物只有一个配方剂量。在这种情况下，`emar_id` 将在 *emar_detail* 表中有两行：一行 `parent_field_ordinal` 为 NULL（通常提供应给药剂量），另一行 `parent_field_ordinal` 为 '1.1'（通常提供实际给药剂量）。

### `administration_type`

给药类型，包括 'IV Bolus'、'IV Infusion'、'Medication Infusion'、'Transdermal Patch' 等。

### `pharmacy_id`
一个标识符，允许将 eMAR 订单与 *pharmacy* 表中提供的药房信息链接起来。注意：在 *emar_detail* 表中，相同的 `emar_id` 可能在不同行中有多个不同的 `pharmacy_id`。

### 其余列
其余列提供有关所给药物的配方剂量交付的信息。
