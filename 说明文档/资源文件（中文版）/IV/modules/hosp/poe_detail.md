
## *poe_detail*

*poe_detail* 表提供了关于 POE 订单的更多信息。该表使用实体-属性-值（EAV）模型：实体是 `poe_id`，属性是 `field_name`，值是 `field_value`。

EAV 表允许在属性异构时灵活地描述实体。

## Links to

* *poe_detail* on `poe_id`


## Table columns

| Name          | Postgres data type    |
|---------------|-----------------------|
| `poe_id`      | VARCHAR(25) NOT NULL  |
| `poe_seq`     | INTEGER NOT NULL      |
| `subject_id`  | INTEGER NOT NULL      |
| `field_name`  | VARCHAR(255) NOT NULL |
| `field_value` | TEXT                  |

### `poe_id`

给定医嘱的唯一标识符。`poe_id` 由 `subject_id` 和一个单调递增的整数 `poe_seq` 
组成，格式为：`subject_id`-`poe_seq`。

### `poe_seq`


一个单调递增的整数，按时间顺序对 POE 医嘱进行排序。也就是说，POE 订单可以按 `poe_seq` 顺序排列。

### `subject_id`
### `field_name`

每一行都提供了关于 POE 医嘱特定方面的详细信息。`field_name` 是赋予该方面的名称。

截至 MIMIC-IV v2.2，下表列出了 `field_value` 中可能的值及其最常见的条目。

| `field_name`        | number of rows | most frequent `field_value` observation   |
|---------------------|----------------|-------------------------------------------|
| Admit to            | 881522         | Medicine                                  |
| Indication          | 27190          | Antibiotics                               |
| Code status         | 197932         | Resuscitate (Full code)                   |
| Transfer to         | 161707         | Medicine                                  |
| Admit category      | 1093726        | Admit to inpatient                        |
| Consult Status      | 36591          | Accepted                                  |
| Discharge When      | 431642         | Discharge Now                             |
| Level of Urgency    | 45617          | Routine (within 24 hours)                 |
| Discharge Planning  | 475428         | Finalized                                 |
| Consult Status Time | 36591          | 2149-12-03 09:00:01                       |
| Tubes & Drains type | 491472         | Indwelling urinary catheter (IUC) - Foley |

### `field_value`

`field_value` 是与给定 POE 医嘱和 `field_name` 相关联的值。例如，对于 `field_name` 为 'Admit to' 
的情况，`field_value` 列包含患者被收治的科室类型（如精神病科、妇科等）。
