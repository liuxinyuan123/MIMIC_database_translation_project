
*admissions* 表提供有关患者入院的信息。由于患者的每次唯一医院就诊都分配有一个唯一的`hadm_id`，因此 *入院* 表可以被视为 `hadm_id` 的定义表。可用信息包括入院和出院的时间信息、人口统计信息、入院来源等。

### 连接至

* *patients* on `subject_id`

## 重要注意事项


* 数据来源于医院的入院、出院和转院（admission, discharge and transfer ）数据库（通常称为“ADT”数据）。
* 器官捐献者账户有时会为在医院死亡的患者创建。这些是不同的住院患者，住院时间非常短，有时是负数。此外，他们的“死亡时间`deathtime`”通常与早期患者入院的“死亡时间`deathtime`”相同。

## 表列

| Name                   | Postgres data type   |
|------------------------|----------------------|
| `subject_id`           | INTEGER NOT NULL     |
| `hadm_id`              | INTEGER NOT NULL     |
| `admittime`            | TIMESTAMP NOT NULL   |
| `dischtime`            | TIMESTAMP            |
| `deathtime`            | TIMESTAMP            |
| `admission_type`       | VARCHAR(40) NOT NULL |
| `admit_provider_id`    | VARCHAR(10)          |
| `admission_location`   | VARCHAR(60)          |
| `discharge_location`   | VARCHAR(60)          |
| `insurance`            | VARCHAR(255)         |
| `language`             | VARCHAR(10)          |
| `marital_status`       | VARCHAR(30)          |
| `race`                 | VARCHAR(80)          |
| `edregtime`            | TIMESTAMP            |
| `edouttime`            | TIMESTAMP            |
| `hospital_expire_flag` | SMALLINT             |

| 字段名                    | Postgres 数据类型        |
|------------------------|----------------------|
| `subject_id`           | INTEGER NOT NULL     |
| `hadm_id`              | INTEGER NOT NULL     |
| `admittime`            | TIMESTAMP NOT NULL   |
| `dischtime`            | TIMESTAMP            |
| `deathtime`            | TIMESTAMP            |
| `admission_type`       | VARCHAR(40) NOT NULL |
| `admit_provider_id`    | VARCHAR(10)          |
| `admission_location`   | VARCHAR(60)          |
| `discharge_location`   | VARCHAR(60)          |
| `insurance`            | VARCHAR(255)         |
| `language`             | VARCHAR(10)          |
| `marital_status`       | VARCHAR(30)          |
| `race`                 | VARCHAR(80)          |
| `edregtime`            | TIMESTAMP            |
| `edouttime`            | TIMESTAMP            |
| `hospital_expire_flag` | SMALLINT             |



## 详细描述


*admissions* 表定义了数据库中的所有住院情况。住院人数被分配一个唯一的随机整数，称为`hadm_id`。

### `subject_id`, `hadm_id`


此表的每一行都包含一个唯一的 '`hadm_id`'，它表示单个患者的入院情况。'`hadm_id`' 的范围是 2000000 - 2999999。此表可能包含重复的 '`subject_id`'，表示单个患者多次入院。可以使用 '`subject_id`' 将 ADMISSIONS 表链接到 PATIENTS 表。

### `admittime`, `dischtime`, `deathtime`

`admitTime`提供患者入院的日期和时间，而`dischTime`提供患者出院的日期和时间。如果适用，`deathtime
`提供患者在医院内死亡的时间。请注意，`deathtime`仅在患者在医院内死亡时出现，并且几乎总是与患者的`dischtime`相同。但是，由于拼写错误，可能会有一些差异。

### `admission_type`


`admission_type`可用于对 ADMISSION 的紧急性进行分类。

有 9 种可能性： 
1. 'AMBULATORY OBSERVATION',
2. 'DIRECT EMER.',
3. 'DIRECT OBSERVATION',
4. 'ELECTIVE', '
5. EU OBSERVATION',
6. 'EW EMER.',
7. 'OBSERVATION ADMIT',
8. 'SURGICAL SAME DAY ADMISSION',
9. 'URGENT'.

### `admit_provider_id`

`admit_provider_id` provides an anonymous identifier for the provider who admitted the patient.  
`admit_provider_id`  为收治患者的提供者提供匿名标识符。


### `admission_location`, `discharge_location`


“`admission_location`”提供有关患者到达医院之前的位置信息。请注意，由于急诊室在技术上是一个诊所，因此通过急诊室入院的患者通常将其作为入院地点。

同样，“`discharge_location`”是患者出院后的处置。

#### 结合UB-04 账单代码

“admission_location”和“discharge_location”与医院内部的“ibax”代码相关联，这些代码在 MIMIC-IV 中没有提供。这些内部代码往往与 UB-04 账单代码一致。

在某些情况下，多个内部代码与给定的 '`admission_location`' 和 '`discharge_location`' 相关联。这可以是做的;1） 医院对同一“`admission_location`”或“`discharge_location`”使用多个代码，或 2） 在去标识化过程中，多个内部代码可能合并为一个“`admission_location`”或“`discharge_location`”。

在下表中，我们为给定的“`admission_location`”和“`discharge_location`”提供了最常见的“ibax”代码的匹配 UB-04 代码（如果适用）。在给出多个代码的情况下，如果此组合是由于上一段中的 1） 造成的，则附加代码必须至少包含最常见代码全部的 10%。

**Admission UB-04 对应表:**

| admission_location                     | UB-04 code(s) |
|----------------------------------------|---------------|
| PHYSICIAN REFERRAL                     | 1, 3          | 
| WALK-IN/SELF REFERRAL                  | 1             |
| AMBULATORY SURGERY TRANSFER            | 1, 2, 6       |
| INFORMATION NOT AVAILABLE              | 1, 9          |
| CLINIC REFERRAL                        | 2, 8          |
| PROCEDURE SITE                         | 2             |
| PACU                                   | 2             |
| TRANSFER FROM HOSPITAL                 | 4, 6          |
| TRANSFER FROM SKILLED NURSING FACILITY | 5             |
| EMERGENCY ROOM                         | 1, 2, 7       |
| INTERNAL TRANSFER TO OR FROM PSYCH     | none          |

| admission_location |UB-04 代码 |
|--------------------|---------------|
| 医生推荐               |1、3 |
| 现场/自助推荐            |1 |
| 门诊手术转移             |1、2、6 |
| 信息不可用              |1、9 |
| 诊所                 |2、8 |
| 手术现场               |2 |
| PACU               |2 |
| 从医院转院              |4、6 |
| 从专业护理机构转入          |5 |
| 急诊室                |1、2、7 |
| 与 PSYCH 之间的内部转移    |none |


**Discharge UB-04 对应表:**

| discharge_location           | UB-04 code(s) |
|------------------------------|---------------|
| HOME                         | 01            |
| ACUTE HOSPITAL               | 02, 81, 86    |
| SKILLED NURSING FACILITY     | 03, 64        |
| ASSISTED LIVING              | 04            |
| HEALTHCARE FACILITY          | 05, 43        |
| HOME HEALTH CARE             | 06            |
| AGAINST ADVICE               | 07            |
| DIED                         | 20            |
| OTHER FACILITY               | 21, 70        |
| HOSPICE                      | 50, 51        |
| REHAB                        | 62            |
| CHRONIC/LONG TERM ACUTE CARE | 63            |
| PSYCH FACILITY               | 65            |
| OTHER FACILITY               | 70            |

| discharge_location |UB-04 代码 |
|--------------------|---------|
| 首页                 |01 |
| 急症医院               |02、81、86 |
| 专业护理机构             |03、64 |
| 生命支持               |04 |
| 医疗保健设施             |05、43 |
| 家庭保健               |06 |
| 反对               |07 |
| 去世                 |20  |
| 其他设施               |21、70 |
| 临终关怀               |50、51 |
| 康复                 |62  |
| 慢性/长期急性护理          |63  |
| 心理设施               |65  |
| 其他设施               |70  |


在线 UB-04 文件通常提供比“`admission_location`”和“`discharge_location`”文本中更多的细节，特别是对于出院患者。

### `insurance`, `language`, `marital_status`, `ethnicity`



`insurance`、`language`、`marital_status`和`ethnicity`列提供有关给定住院的患者人口统计信息。

请注意，由于每次入院都记录了这些数据，因此他们可能会因住院而异。

### `edregtime`, `edouttime`

患者登记和从急诊科出院的日期和时间。


### `hospital_expire_flag`

这是一个二进制标志，指示患者是否在给定的住院治疗范围内死亡。“1”表示在医院死亡，“0”表示存活到出院。
