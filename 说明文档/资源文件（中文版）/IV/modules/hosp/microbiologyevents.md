

## *microbiologyevents*

微生物学检查是一种常见的检查，用于检查感染生长情况，并评估哪种抗生素治疗效果最佳。

该表的最佳解释是通过一个示范性例子。如果为患者请求了血液培养，那么将采集血液样本并送往微生物学实验室。

采集血液样本的时间是 `charttime`。

`spec_type_desc` 将指示这是一个血液样本。

细菌将在血液样本上培养，其余列取决于这种生长的结果：

  如果没有发现生长，其余列将为 NULL。
  
  如果发现细菌，则每个细菌的菌株将出现在 `org_name` 中，导致单个标本产生多行（即给定 `spec_type_desc` 的多行）。
  
  如果对给定的细菌菌株测试抗生素，则每个测试的抗生素将出现在 `ab_name` 列中（即给定 `org_name` 和给定 `spec_type_desc` 的多行）。抗生素参数和敏感性在剩余列中显示（`dilution_text`、`dilution_comparison`、`dilution_value`、`interpretation`）。

## Important considerations

通常，负值由 NULL 值表示。然而，`itemid` 90856 的值为 "NEGATIVE"，应在基于阳性/阴性结果分离微生物学数据的查询中包含它。

`hadm_id` 是通过行政转移表分配给观察值的。然而，这并不总是能完美捕捉到医院停留周围的实验室数据。

具体来说，截至 v2.1，可以使用 `subject_id`、`admittime` 和 `dischtime` 与 *admissions* 表连接，为 1,449,547 个观察值分配 `hadm_id`。然而，只有 1,396,224（96%）个观察值在 *microbiologyevents* 表中实际存储了 `hadm_id`。希望确保捕捉到接近医院停留的实验室数据的用户应意识到这一点，并根据需要使用时间连接。


```
select 
  count(adm.hadm_id) as num_obs_in_hosp
  , count(me.subject_id) as num_obs_with_subject_id
  , count(me.hadm_id) as num_obs_with_hadm_id
  , count(me.hadm_id)*100.0/count(me.subject_id) as percent_obs_assigned_hadm_id
from hosp.admissions adm
left join hosp.microbiologyevents me
on adm.subject_id = me.subject_id
and me.charttime between adm.admittime and adm.dischtime
WHERE me.subject_id IS NOT NULL;
```


## 表列描述

| Name                  | Postgres data type    | Example value                      |
|-----------------------|-----------------------|------------------------------------|
| `microevent_id`       | INTEGER NOT NULL      | 1234567                            |
| `subject_id`          | INTEGER NOT NULL      | 12078372                           |
| `hadm_id`             | INTEGER               | 29450599                           |
| `micro_specimen_id`   | INTEGER NOT NULL      | 6386644                            |
| `order_provider_id`   | VARCHAR(10)           | P12ABC                             |
| `chartdate`           | TIMESTAMP(0) NOT NULL | 2130-04-01 00:00:00                |
| `charttime`           | TIMESTAMP(0)          | 2130-04-01 16:00:00                |
| `spec_itemid`         | INTEGER NOT NULL      | 70012                              |
| `spec_type_desc`      | VARCHAR(100) NOT NULL | BLOOD CULTURE                      |
| `test_seq`            | INTEGER NOT NULL      | 2                                  |
| `storedate`           | TIMESTAMP(0)          | 2130-04-05 00:00:00                |
| `storetime`           | TIMESTAMP(0)          | 2130-04-05 14:46:00                |
| `test_itemid`         | INTEGER               | 90117                              |
| `test_name`           | VARCHAR(100)          | ANAEROBIC BOTTLE                   |
| `org_itemid`          | INTEGER               | 80155                              |
| `org_name`            | VARCHAR(100)          | STAPHYLOCOCCUS, COAGULASE NEGATIVE |
| `isolate_num`         | SMALLINT              | 1                                  |
| `quantity`            | VARCHAR(50)           |                                    |
| `ab_itemid`           | INTEGER               | 90025                              |
| `ab_name`             | VARCHAR(30)           | LEVOFLOXACIN                       |
| `dilution_text`       | VARCHAR(10)           | <=0.12                             |
| `dilution_comparison` | VARCHAR(20)           | <=                                 |
| `dilution_value`      | DOUBLE PRECISION      | 0.12                               |
| `interpretation`      | VARCHAR(5)            | S                                  |
| `comments`            | TEXT                  | ___                                |

### `microevent_id`
一个唯一整数表示该行。

### `subject_id`


### `hadm_id`



### `micro_specimen_id`

唯一地表示了进行微生物学测量的标本。大多数微生物学测量都是基于患者衍生样本（标本）进行的，例如血液、尿液等。

通常会在同一标本上进行多次测量。`micro_specimen_id` 将对同一标本上的测量结果进行分组，例如从同一血液样本中生长的菌株。

### `order_provider_id`

`order_provider_id` 为订购微生物学测试的提供者提供了一个匿名标识符。


## `chartdate`, `charttime`

`charttime` 记录了观察值被记录的时间，通常是实际测量时间的最接近代理。

`chartdate` is the same as `charttime`, except there is no time available.  
`chartdate` 与 `charttime` 相同，只是没有可用的时间。

由于微生物学测量的时间信息并不总是可用的，因此包含了 `chartdate`：为了明确说明何时发生这种情况，`charttime` 为 null，而 `chartdate` 包含测量的日期。

在同时存在 `charttime` 和 `chartdate` 的情况下，`chartdate` 等于 `charttime` 的截断版本（即没有时间信息的 `charttime`）。并非所有观察值都有 `charttime`，但所有观察值都有 `chartdate`。

## `spec_itemid`, `spec_type_desc`

测试细菌生长的标本。

标本是从患者身上采集的样本；例如，血液、尿液、痰等。

## `test_seq`

如果采集了多个样本，`test_seq` 将对它们进行区分。例如，如果对同一标本使用了需氧和厌氧培养瓶，它们将具有不同的 `test_seq` 值（可能是 1 和 2）。

## `storedate`, `storetime`

微生物学结果可用的日期（`storedate`）或日期和时间（`storetime`）。虽然在评估微生物学培养的过程中会提供许多中间结果，但此处的时间是最后一次已知更新的时间。

## `test_itemid`, `test_name`

对给定标本进行的测试。

## `org_itemid`, `org_name`

如果有的话，测试时生长的菌株。如果为 NULL，则没有菌株生长（即阴性培养）。

## `isolate_num`

用于测试抗生素的分离菌落（整数；从 1 开始）。

## `ab_itemid`, `ab_name`

如果对抗生素进行了敏感性测试，抗生素将在此列出。

## `dilution_text`, `dilution_comparison`, `dilution_value`

测试抗生素敏感性时的稀释值。

## `interpretation`

抗生素敏感性的 `interpretation`，并指示测试结果。"S" 表示敏感，"R" 表示耐药，"I" 表示中度敏感，"P" 表示待定。

### `comments`


与微生物学测量相关的去标识化自由文本注释。通常这些提供有关样本的信息，是否已向护理提供者通报了结果，解释考虑因素，或者在某些情况下，注释包含测量结果本身。已完全去标识化的注释（即没有保留任何信息内容）以三个下划线表示：`___`。`NULL` 注释表示该行没有注释。
