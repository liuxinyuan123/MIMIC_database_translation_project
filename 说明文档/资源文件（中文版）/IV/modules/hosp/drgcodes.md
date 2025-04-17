
## *drgcodes*

医院使用诊断相关组 (DRGs) 来为患者的住院治疗获得报销。

这些代码对应于患者在医院停留的主要原因。

## 表列

| Name            | Postgres data type |
|-----------------|--------------------|
| `subject_id`    | INTEGER            |
| `hadm_id`       | INTEGER            |
| `drg_type`      | VARCHAR(4)         |
| `drg_code`      | VARCHAR(10)        |
| `description`   | VARCHAR(195)       |
| `drg_severity`  | SMALLINT           |
| `drg_mortality` | SMALLINT           |

## 详细描述

### `subject_id`
### `hadm_id`
### `drg_type`
用于代码的特定 DRG 本体。

### `drg_code`
DRG 代码。

### `description`
给定 DRG 代码的描述。

### `drg_severity`, `drg_mortality`
某些 DRG 本体进一步量化了患者的病情严重程度和死亡可能性，这些信息在这里记录。
