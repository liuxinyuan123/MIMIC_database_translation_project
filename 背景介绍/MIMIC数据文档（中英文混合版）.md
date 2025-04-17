[TOC]
# MIMIC-IV
### Author 
Alistair Johnson  ,  Lucas Bulgarelli  ,  Tom Pollard  ,  Brian Gow  ,  Benjamin Moody  ,  Steven Horng  ,  Leo Anthony Celi  ,  Roger Mark 

Published: Oct. 11, 2024. Version: 3.1

刘鑫源翻译, 2025-04-15，00点54分

MIMIC-IV v3.1 is now available on BigQuery (Nov. 12, 2024, 4:50 p.m.)
MIMIC-IV v3.1现已在BigQuery上提供（2024年11月12日下午4：50）


MIMIC-IV v3.1现已在BigQuery上提供。用户可以通过PhysioNet请求访问。目前，MIMIC-IV v3.
1在**_mimiciv_v3_1_hosp_** 和 **_mimiciv_v3_1_icu_** 上可用。MIMIC-IV v2.2可在和数据集以及和数据集上使用。2024年11月25日，我们将用MIMIC-IV v3.1替换和上的数据。

Guidelines for creating datasets and models from MIMIC (April 24, 2024, 10:12 a.m.)
从MIMIC创建数据集和模型的指南（2024年4月24日，上午10：12）

我们认识到，创建源自MIMIC或以某种方式增强MIMIC（例如，通过添加注释）的数据集或模型是有价值的。以下是创建这些数据集和模型的一些准则：

任何派生的数据集或模型都应视为包含敏感信息。如果您希望共享这些资源，则应根据与源数据相同的协议在PhysioNet上共享这些资源。

如果您希望在项目名称中使用MIMIC首字母缩写，请包含字母“Ext”（例如，MIMIC-IV-Ext-YOUR-DATASET”）。Ext可以表示“提取”（例如派生子集）或“扩展”（例如注释），这取决于您的用例。

请在准备提交项目时，在提交门户的发现选项卡中选择相关的“父项目”。

使用此资源时，请引用：

Johnson, A., Bulgarelli, L., Pollard, T., Gow, B., Moody, B., Horng, S., Celi, L. A., & Mark, R. (2024). MIMIC-IV (version 3.1). PhysioNet. https://doi.org/10.13026/kpb9-mt58


另外，请引用原始出版物：

Johnson, A.E.W., Bulgarelli, L., Shen, L. et al. MIMIC-IV, a freely accessible electronic health record dataset. Sci Data 10, 1 (2023). https://doi.org/10.1038/s41597-022-01899-x

请包括PhysioNet的标准引文：

Goldberger, A., Amaral, L., Glass, L., Hausdorff, J., Ivanov, P. C., Mark, R., ... & Stanley, H. E. (2000). PhysioBank, PhysioToolkit, and PhysioNet: Components of a new research resource for complex physiologic signals. Circulation [Online]. 101 (23), pp. e215–e220.


## 摘要
回顾性收集的医疗数据有机会通过知识发现和算法开发来改善患者护理。为了最大的公共利益，需要广泛地重复使用医疗数据，但数据共享必须以保护患者隐私的方式进行。在这里，我们展示了重症监护医疗信息市场 （MIMIC-IV），这是一个大型去识别化数据集，其中包含马萨诸塞州波士顿贝斯以色列女执事医疗中心急诊科或重症监护病房收治的患者。MIMIC-IV 包含超过 65,000 名入住 ICU 的患者和超过 200,000 名急诊科收治的患者的数据。MIMIC-IV 整合了现代数据，并采用模块化方法进行数据组织，突出了数据来源，并促进了不同数据源的单独和组合使用。MIMIC-IV 旨在延续 MIMIC-III 的成功并支持医疗保健领域的广泛应用。

## 背景介绍
近年来，医院正在朝着采用数字健康记录系统的方向发展。在美国，2015 年近 96% 的医院拥有数字电子健康记录系统 （EHR） [1]。回顾性收集的医疗数据越来越多地用于流行病学和预测建模。后者部分是由于在大型数据集上建模方法的有效性 [2]。尽管取得了这些进步，但获取医疗数据以改善患者护理仍然是一个重大挑战。虽然限制共享医疗数据的原因有很多方面，但对患者隐私的担忧被强调为最重要的问题之一。尽管患者研究表明，几乎一致认为应该使用去标识化的医疗数据来改善医疗实践，但该领域专家仍在争论这样做的最佳机制。独特的是，MIMIC-III 数据库采用了一种允许访问的方案，允许对数据进行广泛的重用 [3]。这种机制已经成功地在各种研究中广泛使用 MIMIC-III，从在明确定义的队列中评估治疗效果到预测关键患者结果，如死亡率。MIMIC-IV 旨在延续 MIMIC-III 的成功，进行一些更改以提高数据的可用性并支持更多的研究应用。

## 方法


MIMIC-IV 来自两个院内数据库系统：一个定制的医院范围的 EHR 和一个 ICU 特定的临床信息系统。MIMIC-IV 的创建分三个步骤进行：

_**Acquisition**_. Data for patients who were admitted to the BIDMC emergency department or one of the intensive care units were extracted from the respective hospital databases. A master patient list was created which contained all medical record numbers corresponding to patients admitted to an ICU or the emergency department between 2008 - 2022. All source tables were filtered to only rows related to patients in the master patient list.

_**Preparation**_. The data were reorganized to better facilitate retrospective data analysis. This included the denormalization of tables, removal of audit trails, and reorganization into fewer tables. The aim of this process is to simplify retrospective analysis of the database. Importantly, data cleaning steps were not performed, to ensure the data reflects a real-world clinical dataset.

**_Deidentify_**. Patient identifiers as stipulated by HIPAA were removed. Patient identifiers were replaced using a random cipher, resulting in deidentified integer identifiers for patients, hospitalizations, and ICU stays. Structured data were filtered using look up tables and allow lists. If necessary, a free-text deidentification algorithm was applied to remove PHI from free-text. Finally, date and times were shifted randomly into the future using an offset measured in days. A single date shift was assigned to each subject_id. As a result, the data for a single patient are internally consistent. For example, if the time between two measures in the database was 4 hours in the raw data, then the calculated time difference in MIMIC-IV will also be 4 hours. Conversely, distinct patients are not temporally comparable. That is, two patients admitted in 2130 were not necessarily admitted in the same year.

After these three steps were carried out, the database was exported to a character based comma delimited format.

Acquisition。从相应的医院数据库中提取了入住 BIDMC 急诊科或重症监护病房之一的患者的数据。创建了一份主患者名单，其中包含与 2008 年至 2022 
年期间入住 ICU 或急诊科的患者对应的所有病历编号。所有源表都被筛选为仅与主患者列表中的患者相关的行。

Preparation。对数据进行了重新组织，以更好地促进回顾性数据分析。这包括对表进行非规范化、删除审计跟踪以及重新组织为更少的表。此过程的目的是简化数据库的回顾性分析。重要的是，没有执行数据清理步骤，以确保数据反映真实世界的临床数据集。

Deidentify。HIPAA 规定的患者标识符已被删除。使用随机密码替换患者标识符，从而为患者、住院和 ICU 住院患者生成去标识化的整数标识符。使用查找表和 allow 名单筛选结构化数据。如有必要，应用自由文本去标识算法从自由文本中删除 PHI。最后，使用以天为单位的偏移量将日期和时间随机移动到未来。为每个subject_id分配了一个日期班次。因此，单个患者的数据在内部是一致的。例如，如果原始数据中数据库中两个度量之间的时间为 4 小时，则 MIMIC-IV 中计算的时间差也将为 4 小时。相反，不同的患者在时间上没有可比性。也就是说，2130 年入院的两名患者不一定在同一年入院。

执行这三个步骤后，数据库将导出为基于字符的逗号分隔格式。


## 数据描述
MIMIC-IV 分为两个模块：**_hosp_** 和 **_icu_**。将数据组织到这些模块中反映了它们的来源：hosp 模块中的数据来自医院范围的 EHR，而 ICU 模块中的数据来自 ICU 内临床信息系统 （MetaVision）。MIMIC-IV v3.0 中共有 364,627 个唯一个体，每个个体都由一个独特的`subject_id`表示。这些人有 546,028 次住院和 94,458 次独特的 ICU 住院。

### _**hosp**_ 模块
The hosp module contains detailed data regarding 546,028 unique hospitalizations for 223,452 unique individuals. Measurements in the hosp module are predominantly recorded during the hospital stay, though some tables include data from outside an admitted hospital stay as well (e.g. outpatient or emergency department laboratory tests in `labevents`). Patient demographics (`patients`), hospitalizations (`admissions`), and intra-hospital transfers (`transfers`) are recorded in the hosp module. Other information in the hosp module includes laboratory measurements (`labevents`, `d_labitems`), microbiology cultures (`microbiologyevents`, `d_micro`), provider orders (`poe`, `poe_detail`), medication administration (`emar`, `emar_detail`), medication prescription (`prescriptions`, `pharmacy`), hospital billing information (`diagnoses_icd`, `d_icd_diagnoses`, `procedures_icd`, `d_icd_procedures`, `hcpcsevents`, `d_hcpcs`, `drgcodes`), online medical record data (omr), and service related information (services).

_**`hosp`**_ 模块包含有关 223,452 个独特个体的 546,028 例独特住院的详细数据。**`hosp`** 模块中的测量主要在住院期间记录，但有些表格也包含来自入院住院以外的数据（例如，“labevents”中的门诊或急诊科实验室测试）。患者人口统计(`patients`)、住院 (`admissions`)和院内转移 (`transfers`) 记录在 **`hosp`** 模块中。**`hosp`** 模块中的其他信息包括实验室测量（`labevents`, `d_labitems`）、微生物培养物(`microbiologyevents`、`d_micro`)、提供者订单(`poe`, `poe_detail`)、药物管理(`emar`, `emar_detail`)、药物处方 (`prescriptions`, `pharmacy`)、医院账单信息(`diagnoses_icd`, `d_icd_diagnoses`, `procedures_icd`, `d_icd_procedures`, `hcpcsevents`, `d_hcpcs`, `drgcodes`)、在线病历数据  (`omr`) 和服务相关信息(`services`)。

Provider information is available in the provider table. The `provider_id` column is a deidentified character string which uniquely represents a single care provider. As `provider_id` is used in different contexts across the module, a prefix is usually present in data tables to contextualize how the provider relates to the event. For example, the provider who admits the patient to the hospital is documented in the admissions table as `subject_id`. All columns which have a suffix of `provider_id` may be linked to the provider table.

数据提供表中提供了提供数据的人员信息。`provider_id`列是一个去标识化的字符串，且唯一表示单个护理提供者。由于 `provider_id` 用于模块中的不同上下文，因此数据表中通常会出现前缀，以上下文化提供程序与事件的关系。例如，将患者收治入院的提供者在入院表中记录为`subject_id`。后缀为 `provider_id` 的所有列都可以链接到 `provider` 表。


### 去标识化日期和对住院时间一致
All dates in MIMIC-IV have been deidentified by shifting the dates into a 
future time period between 2100 - 2200. This shift is done independently for each patient, and as a result two patients admitted in the deidentified year 2120 cannot be assumed to be admitted in the same year. To provide information about the original time period when a patient was admitted, the patients table provides a set of columns with the "anchor_" prefix. The `anchor_year` column is a deidentified year occurring sometime between 2100 - 2200, and the `anchor_year_group` column is one of the following values: "2008 - 2010", "2011 - 2013", "2014 - 2016", "2017 - 2019", and "2020 - 2022". These pieces of information allow researchers to infer the approximate year a patient received care. For example, if a patient's `anchor_year` is 2158, and their `anchor_year_group` is 2011 - 2013, then any hospitalizations for the patient occurring in the year 2158 actually occurred sometime between 2011 - 2013. In order to minimize accidental release of information, only a single `anchor_year` is provided per subject_id. Consequently, individual stays must be aligned to the anchor year using the respective date (e.g. admittime). Finally, the `anchor_age` provides the patient age in the given `anchor_year`. If the patient was over 89 in the `anchor_year`, this `anchor_age` has been set to 91 (i.e. all patients over 89 have been grouped together into a single group with value 91, regardless of what their real age was).

MIMIC-IV中的所有日期都通过将日期移至2100年至2200年之间的未来时间段进行了去标识化。此偏移是针对每位患者独立进行的，因此在去标识化年份2120年入院的两位患者不能假设在同一年入院。为了提供有关患者入院的原始时间段的信息，患者表提供了一组带有"**_anchor__**"前缀的列。`anchor_year`列是一个去标识化的年份，发生在2100年至2200年之间，而`anchor_year_group`列是以下值之一："2008 - 2010"、"2011 - 2013"、"2014 - 2016"、"2017 - 2019"和"2020 - 2022"。这些信息使研究人员能够推断患者接受护理的大致年份。例如，如果患者的`anchor_year`为2158，且其`anchor_year_group`为2011 - 2013，则该患者在2158年发生的任何住院实际上发生在2011年至2013年之间。为了尽量减少意外信息泄露，每个`subject_id`仅提供一个`anchor_year`。因此，个别住院必须根据相应的日期（例如，入院时间）与`anchor_year`对齐。最后，`anchor_age`提供患者在给定`anchor_year`中的年龄。如果患者在`anchor_year`时超过89岁，则该`anchor_age`已设为91（即所有超过89岁的患者被归为一个值为91的单一组，无论他们的真实年龄是多少）。


### 死亡日期的院外关联
Date of death is available within the dod column of the patients table. Date of death is derived from hospital records and state records. If both exist, hospital records take precedence. State records were matched using a custom rule based linkage algorithm based on name, date of birth, and social security number. State and hospital records for date of death were collected two years after the last patient discharge in MIMIC-IV, which should limit the impact of reporting delays in date of death.

死亡日期可在 _**patients**_ 表的 **_dod_** 列中找到。死亡日期来自医院记录和州记录。如果两者都存在，则 Hospital 记录优先。使用基于姓名、出生日期和社会安全号码的基于自定义规则的链接算法来匹配州记录。在 MIMIC-IV 中，在最后一名患者出院两年后收集死亡日期的州和医院记录，这应该会限制死亡日期报告延迟的影响。

Dates of death occurring more than one year after hospital discharge are censored as a part of the deidentification process. As a result, the maximum time of follow up for each patient is exactly one year after their last hospital discharge. For example, if a patient's last hospital discharge occurs on 2150-01-01, then the last possible date of death for the patient is 2151-01-01. If the individual died on or before 2151-01-01, and it was captured in either state or hospital death records, then the dod column will contain the deidentified date of death. If the individual survived for at least one year after their last hospital discharge, then the dod column will have a NULL value.

作为去标识化过程的一部分，出院后超过一年的死亡日期将被审查。因此，每位患者的最长时间随访时间正好是他们最后一次出院后一年。例如，如果患者最后一次出院发生在 2150-01-01，那么患者最后可能的死亡日期是 2151-01-01。如果个人在 2151 年 1 月 1 日或之前死亡，并且被记录在州或医院的死亡记录中，则 `dod` 列将包含去标识化的死亡日期。如果个人在最后一次出院后存活了至少一年，则 `dod` 列将具有 `NULL` 值。


### **_icu_** 模块
The icu module contains data sourced from the clinical information system known as MetaVision (iMDSoft). MetaVision tables were denormalized to create a star schema where the icustays and d_items tables link to a set of data tables all suffixed with "events". Data documented in the icu module includes intravenous and fluid inputs (`inputevents`), ingredients for the aforementioned inputs (`ingredientevents`), patient outputs (`outputevents`), procedures (`procedureevents`), information documented as a date or time (`datetimeevents`), and other charted information (`chartevents`). All events tables contain a stay_id column allowing identification of the associated ICU patient in _icustays_, and an itemid column allowing identification of the concept documented in `d_items`. Additionally, the caregiver table contains `caregiver_id`, a deidentified integer representing the care provider who documented data into the system. All events tables (`chartevents`, `datetimeevents`, `ingredientevents`, `inputevents`, `outputevents`, `procedureevents`) have a caregiver_id column which links to the caregiver table.

ICU 模块包含来自称为 MetaVision （iMDSoft） 的临床信息系统的数据。MetaVision 表被非规范化以创建星型模式，其中 **_icustays_** 和 **_d_items_** 表链接到一组数据表，所有数据表都以 “_**events**_” 为后缀。ICU 模块中记录的数据包括静脉和液体输入（_**inputevents**_）、上述输入的成分（**_ingredientevents_**）、患者输出（**_outputevents_**）、程序（**_procedureevents_**）、记录为日期或时间的信息（**_datetimeevents_**）和其他图表信息（**_chartevents_**）。所有事件表都包含一个 `stay_id` 列，允许识别 **_icustays_** 中的相关 ICU 患者，以及一个 `itemid` 列，允许识别 `d_items` 中记录的概念。此外，**_caregiver_** 表还包含 `caregiver_id`，这是一个去标识化的整数，表示将数据记录到系统中的护理提供者。所有事件表（**_chartevents_**、**_datetimeevents_**、**_ingredientevents_**、**_inputevents_**、**_outputevents_**、**_procedureevents_**）都有一个链接到 **_caregiver_** 表的 `caregiver_id` 列。

The icu module contains a total of 94,458 ICU stays for 65,366 unique individuals as of MIMIC-IV v3.0. An ICU stay is defined as a contiguous sequence of transfers within a unit of the hospital classified as an ICU, and the _**icustays**_ table is derived from the transfers table. During the creation of the icustays table, consecutive transfers within an ICU were merged into the same `stay_id` for analytical convenience, as these transfers are often bed number changes. Importantly, non-consecutive ICU stays remain as unique `stay_id` in the _**icustays**_ table. In some cases, these could be considered the "same" ICU stay as the patient was transferred out for a planned procedure. In other cases, these are unanticipated readmissions to the ICU. As there was no systematically perfect method to differentiate these cases, we did not attempt to merge non-consecutive `stay_id`, and it is up to the investigator to appropriately handle these cases.

截至 MIMIC-IV v3.0，ICU 模块总共包含 94,458 名独特个体的 65,366 次 ICU 住院。ICU 住院定义为被归类为 ICU 
的医院病房内的连续转移序列，**_icustays_** 表源自转移表。在创建 **_icustays_** 表期间，为了便于分析，ICU 
内的连续转移被合并到同一stay_id，因为这些转移通常是床号变化。重要的是，非连续 ICU 住院在 **_icustays_** 表中仍然是唯一的 
`stay_id`。在某些情况下，这些可以被视为“相同”的 ICU 住院时间，因为患者被转移出去进行计划的手术。在其他情况下，这些是意外的再次入院 ICU。由于没有系统完美的方法来区分这些病例，我们没有尝试合并非连续 `stay_id`，由研究者适当处理这些病例。

### 使用说明
The data described here are collected during routine clinical practice and reflect the idiosyncrasies of that practice. Implausible values may be present in the database as an artifact of the archival process.  Researchers should follow best practice guidelines when analyzing the data.

此处描述的数据是在常规临床实践中收集的，反映了该实践的特性。不可信的值可能作为存档过程的对象存在于数据库中。研究人员在分析数据时应遵循最佳实践指南。

## 文档
Up to date documentation for MIMIC-IV is available on the MIMIC-IV website [4]. We have created an open source repository for the sharing of code and discussion of the database, referred to as the MIMIC Code Repository [5, 6]. The code repository provides a mechanism for shared discussion and analysis of all versions of MIMIC, including MIMIC-IV.

MIMIC-IV 网站 [4] 上提供了 MIMIC-IV 的最新文档。我们创建了一个开源存储库，用于共享代码和讨论数据库，称为 MIMIC 代码存储库 
[5, 6]。代码存储库提供了一种机制，用于共享讨论和分析所有版本的 MIMIC，包括 MIMIC-IV。

## 将 MIMIC-IV 与急诊科、病历和胸部 X 线数据相关联
MIMIC-IV is linkable to other MIMIC projects published on PhysioNet. Where possible, we have prefixed the other projects with "**MIMIC-IV**" to make this clear such as **MIMIC-IV-ED**. Note that **MIMIC-CXR** is also linkable although it is not prefixed with MIMIC-IV. Free-text clinical notes are available in **MIMIC-IV-Note** [7], observations made in the emergency department are available in **MIMIC-IV-ED** [8], and chest x-rays in **MIMIC-CXR** [9].

MIMIC-IV 可链接到 PhysioNet 上发布的其他 MIMIC 项目。在可能的情况下，我们为其他项目加上了 “**MIMIC-IV**” 
的前缀，以明确这一点，例如 **MIMIC-IV-ED**。请注意 **MIMIC-CXR** 也是可链接的，尽管它没有以 **MIMIC-IV** 
为前缀。自由文本临床记录可在**MIMIC-IV-NOTE** [7] 中找到，急诊科的观察结果可在**MIMIC-IV-ED** [8]中找到，胸部X光片可在**MIMIC-CXR** [9]中找到。

Linking the other datasets to MIMIC-IV requires two steps. The first step is to match the data using `subject_id`, taking care to note that MIMIC-IV is a superset of other modules, and sampling biases may be introduced by the linking process. For example, **MIMIC-CXR** is only available between 2011 - 2016 for patients who were admitted to the emergency department, and this selection bias impacts the patient cohort. The second step involves aligning the dates. Since all modules are deidentified by the same shift, the time periods for measurements overlap. For example, if a patient is admitted to the hospital on 2105-01-01, discharged on 2105-01-03, and has an x-ray in **MIMIC-CXR** on 2105-01-02, then it is correct to assume the x-ray was taken while the patient was admitted to the hospital.

将其他数据集链接到 MIMIC-IV 需要两个步骤。第一步是使用 `subject_id` 匹配数据，注意 **MIMIC-IV** 是其他模块的超集，链接过程可能会引入采样偏差。例如，**MIMIC-CXR** 仅在 2011 年至 2016 年期间可用于急诊科收治的患者，这种选择偏倚会影响患者队列。第二步涉及日期对齐。由于所有模块都由同一批次去标识化，因此测量的时间段重叠。例如，如果患者于 2105 年 1 月 1 日入院，于 2105 年 1 月 3 日出院，并在 2105 年 1 月 2 日进行 **MIMIC-CXR** X 光检查，那么假设 X 光片是在患者入院时拍摄的，这是正确的。

## 患者组成
MIMIC-IV contains patients admitted to the emergency department and the intensive care unit. While patients admitted to the intensive care unit must have an associated hospitalization, patients may be admitted to the emergency department without being subsequently admitted to the hospital. As a result, the number of patients in MIMIC-IV is much higher than the number of unique patients with hospitalizations. As of MIMIC-IV v3.0 there are 364,627 unique patients, of whom 223,452 had at least one hospitalization (i.e. at least one record in the admissions table). The remaining 141,175 patients were only seen in the emergency department, which can be verified using the transfers table.

MIMIC-IV 包含入住急诊科和重症监护病房的患者。虽然入住重症监护病房的患者必须接受相关的住院治疗，但患者可以被送入急诊科，而无需随后入院。因此，MIMIC-IV 中的患者人数远高于独特的住院患者人数。截至 MIMIC-IV v3.0，有 364,627 名唯一患者，其中 223,452 名至少有一次住院治疗（即入院表中至少有一条记录）。其余 141,175 名患者仅在急诊科就诊，这可以使用转移表进行验证。

## 病程记录Release
### MIMIC-IV v3.1
MIMIC-IV v3.1 于 2024 年 10 月发布。该版本修复了社区提出的小 bug：

The `itemid` values in the `d_labitems` and labevents tables had changed for a subset of laboratory measurements between v2.2 and v3.0. This change was not intentional. The tables have been updated, and the `d_labitems` and `labevents` itemid values have been verified to be consistent with v2.2.

Two `subject_id` were present in various data tables but were not present in the patients table. These subjects have been removed from the data tables. Database constraints with a foreign key to the `subject_id` column in the patients table should now work correctly.


对于 v2.2 和 v3.0 之间的实验室测量子集，`d_labitems`和 `labevents` 
表中的`itemid`值已更改。这种改变不是有意为之。表已更新，并且已验证`d_labitems`和`labevents`，`itemid` 值与 v2.2 一致。

两个 'subject_id 存在于各种数据表中，但不存在于 patients 表中。这些主题已从数据表中删除。带有 patients 表中 'subject_id' 列的外键的数据库约束现在应该可以正常工作。


If upgrading from v3.0, note that only the following tables were modified (and thus require updating):

如果从 v3.0 升级，请注意，仅修改了以下表（因此需要更新）：

<p>
d_labitems <br>
diagnoses_icd  <br>
drgcodes<br>
labevents<br>
microbiologyevents<br>
omr<br>
transfers<br>
icustays<br>
</p>

## MIMIC-IV v3.0
MIMIC-IV v3.0 was released on July 23, 2024. Stays occurring between 2020 and 2022, inclusive, were added to the database. Out of hospital mortality is available for up to 1-year post hospital or ED discharge. The number of additional patients, admissions, and stays are highlighted by the increased row counts of their respective tables:


patients: 364,627 (was 299,712 in v2.2)
admissions: 546,028 (was 431,231 in v2.2)
icustays: 94,458 (was 73,181 in v2.2)
Other changes include:

MIMIC-IV v3.0 于 2024 年 7 月 23 日发布。2020 年至 2022 年（含）之间的住宿已添加到数据库中。院外死亡率可在出院后或 ED 出院后长达 1 年内获得。额外患者、入院和住院的数量通过各自表的行计数增加来突出显示：

患者：364,627（v2.2 中为 299,712）
入院人数： 546,028 （v2.2 中为 431,231）
ICU患者：94,458（在 v2.2 中为 73,181）
其他更改包括：

Improved language data. The language column of admissions now provides a standardized primary language, if non-English, rather than "?" as before.
Improved insurance data. The categories of the insurance column of admissions have been expanded to "Medicare", "Medicaid", "Private", "Self-pay", "No charge", and "Other". This change better aligns the field with other databases such as the National Inpatient Sample.

改进了语言数据。招生的语言栏现在提供标准化的主要语言（如果不是英语），而不是以前的 “？”。

改进的保险数据。入院保险列的类别已扩展为“Medicare”、“Medicaid”、“Private”、“Self-pay”、“Free charge”和“Other”。此更改更好地使该字段与其他数据库（如 National Inpatient Sample）保持一致。

## MIMIC-IV v2.2
MIMIC-IV v2.2 was released in January 2023. It added provider identifiers, imputed hadm_id for a number of rows in emar, and changed the subset of subject_id which are held out. Final row counts are available in the validation scripts published with the MIMIC Code Repository [6]. For clarity, after removal of the test set, the row counts are as follows:

patients: 299,712 (was 315,460 in v2.0)
admissions: 431,231 (was 454,324 in v2.0)
icustays: 73,181 (was 76,943 in v2.0)

MIMIC-IV v2.2 于 2023 年 1 月发布。它添加了提供程序标识符，为 emar 中的许多行添加了插补`hadm_id`，并更改了保留的`subject_id`子集。最终行计数可在使用 MIMIC 代码存储库 [6] 发布的验证脚本中使用。为清楚起见，删除测试集后，行计数如下所示：

patients：299,712 人（v2.0 中为 315,460 人）

admissions： 431,231 （v2.0 中为 454,324）

icustays：73,181（v2.0 中为 76,943）

### _icu_ 模块
_caregiver_   护理人员    

New table in v2.2. Contains one column: caregiver_id, a deidentified integer which uniquely represents a single caregiver or provider. These identifiers are sourced from the MetaVision ICU system. When present in a table, it indicates the user who documented the data into MetaVision. For example, the caregiver_id associated with a row indicating mechanical ventilation in the **_procedureevents_** table represents the user who documented the event, and not the provider who performed the procedure.  _**chartevents**_, **_datetimeevents_**, **_ingredientevents_**, **_inputevents_**, **_outputevents_**, **_procedureevents_**  added the `caregiver_id` column. This column is a deidentified integer representing the care provider who documented the data for the given row.

v2.2 中的新表。包含一列：`caregiver_id`，一个唯一表示单个护理人员或提供者的去标识化整数。这些标识符来自 MetaVision ICU 系统。当出现在表中时，它表示将数据记录到 MetaVision 中的用户。例如，与 **_procedureevents_** 表中指示机械通气的行关联的`caregiver_id`表示记录事件的用户，而不是执行该过程的提供者。添加了 'caregiver_id` 列。此列是一个去标识化的整数，表示记录给定行数据的护理提供者。



### _hosp module_
#### _provider_   
New table in v2.2. Contains one column: provider_id, a deidentified string which uniquely represents a single caregiver or provider. These identifiers are sourced from the hospital wide EHR system, and used in a variety of contexts across tables in the module.

#### admissions

New column: `admit_provider_id`, a deidentified string representing the provider who admitted the patient.

#### emar

New column: `enter_provider_id`, a deidentified string representing the provider who entered the medication administration information into the database.  

Fixed a bug where a subset of emar rows (713,117, ~2.5%) did not have an hadm_id even though they were associated with a given hospitalization. These rows occur outside of the administratively documented admission and discharge times for a hospitalization, but are still considered as administered during that hospitalization in the raw data.

#### labevents, microbiologyevents, poe, prescriptions

New column: order_provider_id, a deidentified string representing the provider who ordered the corresponding event (e.g. the lab test in the case of labevents, or the medication in the case of prescriptions).

## MIMIC-IV v2.1
MIMIC-IV v2.1 was released on November 16, 2022. It removed a subset of subject_id which will be retained internally as a test set. Future data releases will exclude these patients.

_patients_ - Removed 15,748 subject_id from the table   
_admissions_ - Removed 23,093 hadm_id from the table.   
_icustays_ - Removed 3,762 stay_id from the table.     
Other tables will have rows removed to reflect the removal of the aforementioned subject_id, hadm_id, and stay_id. Final row counts are available in the validation scripts published with the MIMIC Code Repository [6].

## MIMIC-IV v2.0
MIMIC-IV v2.0 was released on June 12, 2022. It focused on expanding the data elements available for patients within MIMIC-IV v1.0. Additional data available includes out-of-hospital date of death, information from the online medical record system (which includes height and weight), and more detail for continuous infusions in the ICU.

### Major changes
The core module has been removed to simplify the schema. The admissions, 
patients, and transfers tables are now in the hosp module.    
Neonates have been removed from the dataset. Neonatal data will be released 
in a separate project with data from the neonatal intensive care unit.     
### icu module
_icustays_     
Around 700 stays (~1%) have changed due to the changes in the patients table.

_chartevents, d_items_     
The problem list from MetaVision has been added. All problems are documented 
with the same itemid now present in `d_items`: 220001. There are just over 1,
000 unique problems. Most documented problems are related to the care plan 
for the patient and documented during nurse shift changes (either 7am or 7pm)
. Less frequently, the ongoing issues are documented here.      
_ingredientevents_     
This is a new table associated with inputevents. Each intravenous administration tracked in inputevents is associated with a set of ingredients. These ingredients include water content, caloric information, and so on. The goal of the inputevents table is to support nutrition research and to provide a mechanism for estimating fluid input via summing all instances of the water ingredient. These ingredients have been separated from the inputevents table to simplify analysis and reduce the size of inputevents.
inputevents
Removed a single column which contained only null values: cancelreason.
procedureevents
Removed columns which contained only null values: totalamount, totalamountuom, cancelreason, comments_editedby, comments_canceledby, comments_date, secondaryordercategoryname.

### hosp module
admissions
Fixed an issue where hospitalizations were missing edregtime and edouttime when the patient was admitted via the ED (reported in #1247, thanks @MEladawi).
patients
dod is now populated with out-of-hospital mortality from state death records. For patients admitted to the ICU, this change has increased capture of date of death from 8,223 records to 23,844 (i.e. we now have out-of-hospital mortality for an additional 15,621 ICU patients).
The mechanism for determining patients included in MIMIC was changed. For the most part this has resulted in an improvement, particularly regarding the logic for merging patients who had distinct medical record numbers. As a result of this change, most tables have had a change in the data content. Approximately 1% of stays were affected.
transfers
Fixed a bug where the outtime for ED stays with no associated hadm_id (i.e. an ED stay where the individual was not admitted to the hospital) was incorrect. This resulted in all transfers rows with a NULL hadm_id having an apparent stay of minutes or less. The outtime column has now been corrected.
labevents, d_labitems
The itemid for d_labitems has been changed for 43 items. These are extremely infrequently documented and each itemid has fewer than 100 observations in labevents. The exact itemid are provided in the changelog file CHANGELOG.txt.
Errors were found in the current values of loinc_code (reported in #938, thanks @Mauvila). In order to enable collaborative improvement, the loinc_code column has been removed, and will now be collaboratively developed in the MIMIC Code Repository. Initial values will be sourced from the hospital system.
A number of labs which previously had the value in the comments field now have the value in the value field (reported in #941, thanks @Mauvila). This change makes the labevents table more consistent with MIMIC-III, which had these values in the value field.
microbiologyevents
New organisms, tests, specimens, and antibiotics have been added.
omr
A new table has been added: omr. The source of this data is the Online Medical Record, and it contains miscellaneous information useful for understanding an individual's health. As of v2.0, the omr table has the following information: blood pressure, height, weight, body mass index, and Estimated Glomerular Filtration Rate (eGFR). These values are available from both inpatient and outpatient visits, and in many cases a "baseline" value from before a patient's hospitalization is available.
prescriptions
The formulary_drug_cd table has been added back (was previously in MIMIC-III). This column has the same set of values as the product_code column of emar_detail.

## MIMIC-IV v1.0
MIMIC-IV v1.0 was released March 16, 2021.

### core
admissions
A number (~1000, <1%) of erroneous hadm_id have been removed.
patients
dod is now populated using the patient's deathtime from their latest hospitalization (reported in #71, thanks @jinjinzhou).
At the moment, out-of-hospital mortality is not captured by `dod`.
transfers
Removed erroneous transfers included in the previous version.
transfer_id has been regenerated. transfer_id in MIMIC-IV v1.0 are not compatible with transfer_id from v0.4. We do not intend to change transfer_id when updating MIMIC-IV, but had to update it due to an error in its generation.
All hadm_id in transfers are also present in admissions and vice-versa (reported in #84, thanks @kokoko12305).
### icu
_icustays_    
ICU stays were inappropriately assigned in the previous version due to an error in the preprocessing code. Previously, non-ICU ward transfers were included in the ICU stays, and certain ward stays were not treated as ICU stays (reported in #67, thanks @JHLiu7 and @stefanhgm). The assignment of stay_id has been regenerated.
The mapping between hospital transfers and ICU stays has been updated.
stay_id in MIMIC-IV v1.0 are not compatible with stay_id from v0.4. We do not intend to change stay_id when updating MIMIC-IV, but had to update it due to the error identified above.
The change in icustays has re-assigned values to new stay_id, as a result all tables have had their content changed (due to a change in stay_id), but the structure is unchanged.
### hosp
_hcpcsevents_    
Data has been added for a number of previously excluded hospitalizations.
The table now has a chartdate column, containing the date associated with the code. Every row is associated with a date.
drgcodes
Data has been added for a number of previously excluded hospitalizations.
Duplicate DRG codes have been removed from the table.
Descriptions have been updated using the latest dictionaries made available from mass.gov and HCUP.
diagnoses_icd, d_icd_diagnoses
Data has been added for a number of previously excluded hospitalizations (reported in #27, thanks @yugangjia).
The icd_code column is now trimmed and stored as a VARCHAR, i.e. codes no longer contain trailing whitespaces ('850 ' -> '850').
Missing ICD codes have been added to the dictionary. All ICD codes in the diagnoses_icd table have an associated reference in d_icd_diagnoses.
labevents
The comments field has been updated, fixing a bug where comments longer than 4096 characters were truncated. Due to the deidentification, it's unlikely users will see much difference, as these comments will appear as ___.
procedures_icd
Data has been added to procedures_icd for a number of previously excluded hospitalizations.
The table now has a chartdate column, containing the date associated with each billed procedure.
The icd_code column is now trimmed and stored as a VARCHAR, i.e. codes no longer contain trailing whitespaces ('850 ' -> '850').
Missing ICD codes have been added to the dictionary. All ICD codes in the procedures_icd table have an associated reference in d_icd_procedures.

### v0.4
d_micro
This table has been removed
microbiologyevents
Added the column spec_type_desc, test_name, org_name, and ab_name columns
These columns contain the textual name of the organism/antibiotic/test/specimen
Added the comments column: this column contains information about the test, and in some cases (e.g. viral load tests), contains the result
### v0.3
Fixed a bug in the timing between hosp and icu
### v0.2
Updated demographics in the patient table   
anchor_year -> anchor_year_group   
anchor_year_shifted -> anchor_year   
See the patients table in the MIMIC online documentation for detail on these columns
transfers
Deleted the los column
emar
mar_id -> emar_id
emar_id is now a composite of subject_id and emar_seq, and has form “subject_id-emar_seq”
emar_seq column - a monotonically increasing integer starting with the first eMAR administration
Added poe_id and pharmacy_id columns for linking to those tables
emar_detail
mar_id -> emar_id (changed as above)
Deleted the mar_detail_id column
hcpcsevents
ticket_id_seq -> seq_num
labevents
Many previously NULL values are now populated - these were removed originally due to deidentification
Added the comments column. This contains deidentified free-text comments with labs. PHI is replaced with three underscores (___). If an entire comment is ___, then the entire comment was scrubbed.
microbiologyevents
stay_id column removed
spec_id -> micro_specimen_id
Added the poe and poe_detail tables
Documentation of provider orders for various treatments and other aspects of patient management
Added the prescriptions table
Documentation of medicine prescriptions via the provider order interface
Added the pharmacy table
Detailed information regarding prescriptions provided by the pharmacy including formulary dose, route, frequency, dose, and so on.
inputevents
Fixed an error in the calculation of the amount column
icustays
Re-derived stay_id - the new stay_id are distinct from the previous version.
## 伦理
The collection of patient information and creation of the research resource was reviewed by the Institutional Review Board at the Beth Israel Deaconess Medical Center, who granted a waiver of informed consent and approved the data sharing initiative.

贝斯以色列女执事医疗中心的机构审查委员会审查了患者信息的收集和研究资源的创建，该委员会批准了知情同意的豁免并批准了数据共享计划。


## 致谢

We would like to thank the Beth Israel Deaconess Medical Center for their continued support of the MIMIC project. In particular we would like to thank Carolyn Conti, Alvin Gayles, Larry Markson, Ayad Shammout, Lu Shen, and Manu Tandon for their assistance. This work was supported by the National Institute of Biomedical Imaging and Bioengineering (NIBIB) under NIH grant number R01EB030362.

我们要感谢 Beth Israel Deaconess Medical Center 对 MIMIC 项目的持续支持。我们特别要感谢 Carolyn Conti、Alvin Gayles、Larry Markson、Ayad Shammout、Lu Shen 和 Manu Tandon 的帮助。这项工作得到了美国国家生物医学成像和生物工程研究所 （NIBIB） 的支持，NIH 资助号 R01EB030362。

## 利益冲突
无披露。

## 参考文献
Henry, J., Pylypchuk, Y., Searcy T. & Patel V. (May 2016). Adoption of Electronic Health Record Systems among U.S. Non-Federal Acute Care Hospitals: 2008-2015. ONC Data Brief, no.35. Office of the National Coordinator for Health Information Technology: Washington DC.+
Halevy, A., Norvig, P., & Pereira, F. (2009). The unreasonable effectiveness of data. IEEE Intelligent Systems, 24(2), 8-12.
Johnson, A. E., Pollard, T. J., Shen, L., Lehman, L.H., Feng, M., Ghassemi, M., ... & Mark, R. G. (2016). MIMIC-III, a freely accessible critical care database. Scientific data, 3(1), 1-9.
MIMIC Online Documentation. https://mimic.mit.edu
Johnson AE, Stone DJ, Celi LA, Pollard TJ. The MIMIC Code Repository: enabling reproducibility in critical care research. Journal of the American Medical Informatics Association. 2018 Jan;25(1):32-9.
Alistair Johnson, Tom Pollard, Jim Blundell, Brian Gow, erinhong, Nicolas Paris, et al. MIT-LCP/mimic-code: MIMIC Code v2.1.1. Zenodo; 2021. https://doi.org/10.5281/zenodo.821871
Johnson, A., Pollard, T., Horng, S., Celi, L. A., & Mark, R. (2023). MIMIC-IV-Note: Deidentified free-text clinical notes (version 2.2). PhysioNet. https://doi.org/10.13026/1n74-ne17
.
Johnson, A., Bulgarelli, L., Pollard, T., Celi, L. A., Mark, R., & Horng, S. (2023). MIMIC-IV-ED (version 2.2). PhysioNet. https://doi.org/10.13026/5ntk-km72
.
Johnson, A., Pollard, T., Mark, R., Berkowitz, S., & Horng, S. (2019). MIMIC-CXR Database (version 2.0.0). PhysioNet. https://doi.org/10.13026/C2JT1Q
