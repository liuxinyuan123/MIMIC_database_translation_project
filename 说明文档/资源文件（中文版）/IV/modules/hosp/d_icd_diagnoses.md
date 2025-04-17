

## The *d_icd_diagnoses* table

此表定义了国际疾病分类 （ICD） 第 9 版和第 10 版的 **诊断** 代码。这些代码在患者住院结束时分配，并由医院用于为所提供的护理开具账单。

### 表连接

* *diagnoses_icd* ON `icd_code` and `icd_version`

<!-- # Important considerations -->

## 表列描述

| 名称            | Postgres 数据类型    |
|---------------|------------------|
| `icd_code`    | CHAR(7) NOT NULL |
| `icd_version` | INTEGER NOT NULL |
| `long_title`  | VARCHAR(255)     |

## 详细描述

### `icd_code`, `icd_version`


`icd_code` 国际疾病分类 （ICD）代码.

此编码系统有两个版本：版本 9 （ICD-9） 和版本 10 （ICD-10）。这些可以使用 `icd_version` 列进行区分。

ICD-9 和 ICD-10 代码通常都以小数表示。解释 ICD 代码时不需要这个小数;即 '0010' 的 `icd_code` 等同于 '001.0'。

ICD-9 和 ICD-10 代码具有不同的格式：ICD-9 代码是 5 个字符长的字符串，完全是数字（前缀为“E”或“V”的代码除外，这些代码用于伤害的外部原因或补充分类）。重要的是，ICD-9 代码在数据库中保留为字符串，因为代码中的前导 0 有意义。

ICD-10 代码是 3-7 个字符长，并且总是以字母开头，后跟一组数字。



### `long_title`

`long_title`提供了 ICD 代码的含义。例如，ICD-9 代码 _0010_ 有`long_title` “霍乱弧菌引起的霍乱”。
