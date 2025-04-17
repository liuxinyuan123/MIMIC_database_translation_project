

Hosp 模块提供从全院电子健康记录中获取的所有数据。涵盖的信息包括患者和入院信息、实验室测量、微生物学、药物管理和计费诊断。

-----



hosp 模块包含从医院范围的 EHR 派生的数据。这些测量结果主要在住院期间记录，但有些表格也包括来自医院外的数据(例如 _**labevents**_ 中的门诊实验室检查)。


### 详细信息，包括患者和入院详细信息

- **_[patients](./patients.md)_**
- **_[admissions](./admissions.md)_**
- **_[transfers](./transfers.md)_**


### 实验室检查
- **_[labevents](./labevents.md)_**
- **_[d_labitems](./d_labitems.md)_**


### 微生物培养
- **_[microbiologyevents](./microbiologyevents.md)_**


###  护理提供者
- **_[poe](./poe.md)_**
- **_[poe_detail](./poe_detail.md)_**


### 药物管理
- **_[emar](./emar.md)_**
- **_[emar_detail](./emar_detail.md)_**

### 药物处方
- **_[prescriptions](./prescriptions.md)_**
- **_[pharmacy](./pharmacy.md)_**

### 医院账单信息
- **_[diagnoses_icd](./diagnoses_icd.md)_**
- **_[d_icd_diagnoses](./d_icd_diagnoses.md)_**
- **_[procedures_icd](./procedures_icd.md)_**
- **_[d_icd_procedures](./d_icd_procedures.md)_**
- **_[hcpcsevents](./hcpcsevents.md)_**
- **_[d_hcpcs](./d_hcpcs.md)_**
- **_[drgcodes](./drgcodes.md)_**


### 医院服务相关信息
- **_[services](./services.md)_**


### Hosp

#### [omr ](./omr.md)table
在线病历 (OMR) 表包含来自 EHR 的杂项信息。


#### [provider](./provider.md) table

provider 表列出了数据库中使用的去标识化提供者标识符。


#### [admissions](./admissions.md) table

有关住院患者的详细信息。

#### [d_hcpcs](./d_hcpcs.md) table 

hcpcsevents 的维度表;提供 CPT 代码的描述。


#### [d_icd_diagnoses](./d_icd_diagnoses.md) table 

diagnoses_icd 的维度表;提供 ICD-9/ICD-10 计费诊断的描述。


####   [d_icd_procedures](./d_icd_procedures.md) table 

procedures_icd 的维度表;提供 ICD-9/ICD-10 计费程序描述。

#### [d_labitems](./d_labitems.md)

labevents 的维度表;提供所有实验室项目的描述。

#### [diagnoses_icd](./diagnoses_icd.md)

住院的计费 ICD-9/ICD-10 诊断。



#### [drgcodes](./drgcodes.md)

住院的计费诊断相关组 (DRG) 代码。

#### [emar](./emar.md)

电子药物管理记录 (eMAR);给药时对药物进行条形码扫描。

#### [emar_detail](./emar_detail.md)

emar 中记录的电子管理的补充信息。


#### [hpcsevents](./hcpcsevents.md)

住院期间发生的计费事件。包括 CPT 代码。

#### [labevents](./labevents.md)

实验室测量数据来源于患者来源的标本。


#### [microbiologyevents](./microbiologyevents.md)
微生物培养。


#### [patients](./patients.md) table
患者的性别、年龄和死亡日期(如果有信息)。


#### [pharmacy](./pharmacy.md)
处方集、剂量和处方药的其他信息。


#### [poe](./poe.md)
由医嘱提供者发出的与患者护理相关的医嘱。

#### [poe_detail](./poe_detail.md)
医院提供者下达的医嘱的补充信息。

#### [prescriptions](./prescriptions.md)
处方药。

#### [procedures_icd](./procedures_icd.md)
患者住院期间的计费项目。

#### [services](./services.md)
在患者住院期间照顾患者的医院服务。

#### [transfers](./transfers.md) table
有关患者院内科室转移的详细信息。
