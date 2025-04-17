
## *omr*

The Online Medical Record (OMR) table stores miscellaneous information 
documented in the electronic health record.   
It is a useful source of outpatient measurements such as blood pressure, weight, height, and body mass index.

在线病历 (OMR) 表存储电子健康记录中记录的杂项信息。   
它是门诊测量的有用来源，例如血压、体重、身高和体重指数。

## Table columns
## 表格列

| Name           | Postgres data type    |
|----------------|-----------------------|
| `subject_id`   | INTEGER NOT NULL      |
| `chartdate`    | DATE NOT NULL         |
| `seq_num`      | INTEGER NOT NULL      |
| `result_name`  | VARCHAR(100) NOT NULL |
| `result_value` | TEXT NOT NULL         |

|姓名 |Postgres 数据类型 |
|----------|-----------------------|
|`subject_id` |整数非 NULL |
|`chartdate` |日期不为空 |
|`seq_num` |整数非 NULL |
|`result_name` |VARCHAR(100) 非 NULL |
|`result_value` |文本不为空 |

## Detailed Description
## 详细说明

### `subject_id`

{{% include "/static/include/subject_id.md" %}}

## `chartdate`
The date on which the observation was recorded.   
记录观察结果的日期。


## `seq_num`

An monotonically increasing integer which uniquely distinguishes results of the same type recorded on the same day.   

For example, if two blood pressure measurements occur on the same day, `seq_num` orders them chronologically.

一个单调递增的整数，用于唯一区分同一天记录的相同类型的结果。   
例如，如果在同一天进行两次血压测量，则 'seq_num' 会按时间顺序排列它们。


## `result_name`

Each row provides detail regarding a single observation in the EHR.  `result_name` provides a human interpretable description of the observation. As of MIMIC-IV v2.2, the following table lists the number of observations and the most common value.

每行提供有关 EHR 中单个观察的详细信息。`result_name`提供了对观察的人类可解释描述。从 MIMIC-IV v2.2 开始，下表列出了观测值的数量和最常见的值。

| result_name                      | number of observations | example value |
|----------------------------------|------------------------|---------------|
| eGFR                             | 240                    | >60           |
| Blood Pressure Lying             | 2764                   | 120/70        |
| Blood Pressure Sitting           | 3400                   | 120/70        |
| Blood Pressure Standing (1 min)  | 2560                   | 90/60         |
| Blood Pressure Standing          | 523                    | 110/70        |
| Blood Pressure Standing (3 mins) | 626                    | 80/50         |
| BMI (kg/m2)                      | 1662112                | 26.6          |
| Weight (Lbs)                     | 1889542                | 150           |
| Blood Pressure                   | 2169549                | 110/70        |
| Height (Inches)                  | 706906                 | 64            |
| BMI                              | 554                    | 25.0          |
| Weight                           | 354                    | 150.00        |
| Height                           | 39                     | 64.50         |


| result_name   | 观测值个数   | 示例值    |
|---------------|---------|--------|
| eGFR (肾小球滤过率) | 240     | >60    |
| 立位血压          | 2764    | 120/70 |
| 坐位血压          | 3400    | 120/70 |
| 站立式血压 (1 分钟)  | 2560    | 90/60  |
| 站立血压          | 523     | 110/70 |
| 站立式血压 (3 分钟)  | 626     | 80/50  |
| 体重指数 (kg/m2)  | 1662112 | 26.6   |
| 重量 (磅)        | 1889542 | 150    |
| 血压            | 2169549 | 110/70 |
| 高度 (英寸)       | 706906  | 64     |
| 体重指数          | 554     | 25.0   |
| 重量            | 354     | 150,00 |
| 身高            | 39      | 64.50  |


### `result_value`

`result_value` is the value associated with the given OMR observation. For example, for the `result_name` of 'Blood Pressure', the `field_value` column contains the recorded blood pressure (120/80, 130/70, and so on).

`result_value`是与给定 OMR 观察值关联的值。例如，对于 'Blood Pressure' 的 'result_name'，'field_value' 列包含记录的血压(120/80、130/70 等)。
