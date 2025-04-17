**MIMIC-IV** is a relational database containing real hospital stays for patients admitted to a tertiary academic medical center in Boston, MA, USA. **MIMIC-IV** contains comprehensive information for each patient while they were in the hospital: laboratory measurements, medications administered, vital signs documented, and so on.
The database is intended to support a wide variety of research in healthcare.
MIMIC-IV builds upon the success of **MIMIC-III**, and incorporates numerous improvements over **MIMIC-III**.

**MIMIC-IV** 是一个关系数据库，包含美国马萨诸塞州波士顿一家三级学术医疗中心收治的患者的真实住院时间。**MIMIC-IV** 包含每位患者在医院期间的全面信息：实验室测量、给药、记录的生命体征等。
该数据库旨在支持医疗保健领域的各种研究。
**MIMIC-IV** 建立在 **MIMIC-III** 的成功之上，并结合了对 **MIMIC-III**的许多改进。

MIMIC-IV is separated into "modules" to reflect the provenance of the data. There are currently five modules:

**MIMIC-IV** 被分成 `模块` 以反映数据的来源。目前有五个模块(`module`)：


- [hosp](./modules/hosp/_index.md) - hospital level data for patients: labs, micro,  and  electronic medication administration
- [icu](./modules/icu/_index.md) - ICU level data. These are the event tables, and are identical in structure to MIMIC-III (chartevents, etc)
- [ed](./modules/ed/_index.md) - data from the emergency department
- [cxr](./modules/cxr/_index.md) - lookup tables and meta-data from MIMIC-CXR, allowing linking to MIMIC-IV
- [note](./modules/note/_index.md) - deidentified free-text clinical notes

---

- [hosp](./modules/hosp/_index.md) - 患者医院级别的数据：实验室、微生物、电子药物管理
- [icu](./modules/icu/_index.md) - ICU 级别数据。这些是事件表，在结构上与 MIMIC-III (`chartevents` 等) 相同
- [ed](./modules/ed/_index.md) - 来自急诊科的数据
- [cxr](./modules/cxr/_index.md) - 来自 MIMIC-CXR 的查找表和元数据，允许链接到 MIMIC-IV
- [note](./modules/note/_index.md) - 去标识化的自由文本临床笔记

---

MIMIC-Note is currently not publicly available and the structure is subject to change.

MIMIC-Note 目前尚未公开可用，其结构可能会发生变化。

---

All patients across all datasets are in the [hosp](./modules/hosp) module. 

However, not all ICU patients have ED data, not all ICU patients have CXRs, not all ED patients have hospital data, and so on. Within an individual dataset, there are also incomplete tables as certain electronic systems did not exist in the past, particularly the eMAR system.

Tables for each module are detailed in the respective sections.


所有数据集中的所有患者都在 [hosp](./modules/hosp/_index.md) 模块中。

然而，并非所有 ICU 患者都有 ED 数据，并非所有 ICU 患者都有 CXR，并非所有 ED 患者都有医院数据，等等。在单个数据集中，也存在不完整的表格，因为某些电子系统在过去不存在，尤其是 eMAR 系统。

每个模块的表格在相应的部分中有详细介绍。
