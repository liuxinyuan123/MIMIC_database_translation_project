
## *diagnoses_icd*

在常规医院护理中，患者因与住院相关的诊断而被医院收费。

此表记录了患者在住院期间使用 ICD-9 和 ICD-10 本体被收费的所有诊断。

诊断是在医院出院时开具的，由阅读签名临床笔记的训练有素的人确定。

### **链接到**

* *d_icd_diagnoses* 表的 `icd_code` 和 `icd_version`

## Table columns

| Name          | Postgres data type |
|---------------|--------------------|
| `subject_id`  | INTEGER NOT NULL   |
| `hadm_id`     | INTEGER NOT NULL   |
| `seq_num`     | INTEGER NOT NULL   |
| `icd_code`    | VARCHAR(7)         |
| `icd_version` | INTEGER            |

**表列**

| 名称            | PostgreSQL 数据类型  |
|---------------|------------------|
| `subject_id`  | INTEGER NOT NULL |
| `hadm_id`     | INTEGER NOT NULL |
| `seq_num`     | INTEGER NOT NULL |
| `icd_code`    | VARCHAR(7)       |
| `icd_version` | INTEGER          |

## 详细描述

### `subject_id`
### `hadm_id`
### `seq_num`
分配给诊断的优先级。

优先级可以解释为对哪些诊断是“重要”的排名，但对这一广泛陈述存在许多限制。

例如，被诊断为败血症的患者必须将败血症作为其 *第2* 项开具的条件。第1项开具的条件必须是感染源。

对低优先级诊断的正确排名也较少重视（因为例如，第5-10项诊断代码的优先级可能没有正确的排序）。

### `icd_code`, `icd_version`

`icd_code` 是国际编码定义 (ICD) 代码。

此编码系统有两个版本：版本 9（ICD-9）和版本 10（ICD-10）。可以使用 `icd_version` 列来区分它们。

通常，ICD-10 代码更详细，尽管存在将 ICD-9 代码转换为 ICD-10 代码的代码映射（或“交叉引用”）。

ICD-9 和 ICD-10 代码通常以小数形式表示。解释 ICD 代码时不需要这个小数；例如，`icd_code` 为 '0010' 等同于 '001.0'。
