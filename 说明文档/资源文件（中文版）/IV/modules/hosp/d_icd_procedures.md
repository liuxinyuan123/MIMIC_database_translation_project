
  *procedures_icd* 的维度表;提供了 ICD-9/ICD-10 计费程序的描述。


## *d_icd_procedures* 表


下表定义了 **治疗操作** 的国际疾病分类 （ICD） 
代码。这些代码在患者住院结束时分配，并由医院用于为所提供的护理开具账单。它们可以进一步用于确定是否进行了某些程序（例如 手术）。


### 表连接

* *procedures_icd* on `icd_code` and `icd_version`


## 表列描述

| 字段            | Postgres 数据类型    |
|---------------|------------------|
| `icd_code`    | CHAR(7) NOT NULL |
| `icd_version` | INTEGER NOT NULL |
| `long_title`  | VARCHAR(255)     |

## 详细描述

### `icd_code`, `icd_version`

`icd_code` 是国际疾病分类 （ICD） 代码


此编码系统有两个版本：版本 9 （ICD-9） 和版本 10 （ICD-10）。这些可以使用 '`icd_version`' 列进行区分。一般来说，ICD-10 代码更详细，尽管存在将 ICD-9 代码转换为 ICD-10 代码的代码映射（或“cross-walks”）。

ICD-9 和 ICD-10 代码通常都以小数表示。解释 ICD 代码时不需要这个小数;即 '0010' 的 '`icd_code`' 等同于 '001.0'。

## `long_title`
`long_title` 提供了给定程序代码的简要定义。
