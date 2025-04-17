

患者一生中保持一致的信息存储在此表中。

## Table columns

| Name                | Postgres data type    |
|---------------------|-----------------------|
| `subject_id`        | INTEGER NOT NULL      |
| `gender`            | VARCHAR(1) NOT NULL   |
| `anchor_age`        | INTEGER NOT NULL      |
| `anchor_year`       | INTEGER NOT NULL      |
| `anchor_year_group` | VARCHAR(255) NOT NULL |
| `dod`               | TIMESTAMP(0)          |

## 详细描述

### `subject_id`

`subject_id` 是一个唯一标识符，用于指定单个患者。与单个 `subject_id` 关联的任何行都属于同一个个体。由于 `subject_id` 是表的主键，因此它对每一行都是唯一的。

### `gender`

`gender` 是患者的基因型性别。

### `anchor_age`, `anchor_year`, `anchor_year_group`

这些列提供了有关患者入院时的实际年份以及患者当时年龄的信息。

[//]: # (* `anchor_year` is a shifted year for the patient.)
* `anchor_year` 是患者的偏移年份。

[//]: # (* `anchor_year_group` is a range of years - the patient's `anchor_year` occurred during this range.)
* `anchor_year_group` 是一个年份范围 - 患者的 `anchor_year` 发生在此范围内。

[//]: # (* `anchor_age` is the patient's age in the `anchor_year`. If a patient's `anchor_age` is over 89 in the `anchor_year` then their `anchor_age` is set to 91, regardless of how old they actually were.)
* `anchor_age` 是患者在 `anchor_year` 中的年龄。如果患者的 `anchor_age` 在 `anchor_year` 中超过 89 岁，则无论他们实际年龄多大，`anchor_age` 都将设置为 91。

[//]: # (* Example: a patient has an `anchor_year` of 2153, `anchor_year_group` of 2008 - 2010, and an `anchor_age` of 60.)
* 例如：一个患者的 `anchor_year` 为 2153，`anchor_year_group` 为 2008 - 2010，`anchor_age` 为 60。

[//]: # (  * The year 2153 for the patient corresponds to 2008, 2009, or 2010.)
  * 患者的 2153 年对应于 2008、2009 或 2010 年。

[//]: # (  * The patient was 60 in the shifted year of 2153, i.e. they were 60 in 2008, 2009, or 2010.)
  * 患者在偏移年份 2153 年为 60 岁，即他们在 2008、2009 或 2010 年为 60 岁。

[//]: # (  * A patient admission in 2154 will occur in 2009-2011, an admission in 2155 will occur in 2010-2012, and so on.)
  * 2154 年的患者入院将发生在 2009-2011 年，2155 年的入院将发生在 2010-2012 年，依此类推。

### `dod`

患者的去标识化死亡日期。死亡日期从两个来源提取：医院信息系统和[马萨诸塞州生命记录和统计登记处Massachusetts State Registry of Vital Records and Statistics](https://www.mass.gov/orgs/registry-of-vital-records-and-statistics)。

MIMIC 中的个体患者记录通过基于标识符（包括姓名、社会安全号码和出生日期）的自定义算法与生命记录进行匹配。


由于这种链接，MIMIC-IV 患者的院外死亡率数据可提供至**出院后一年**。所有发生在出院后一年以上的患者死亡都被截断。

生存研究应将其纳入设计。
