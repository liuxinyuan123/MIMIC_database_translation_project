
**MIMIC-IV** 是一个关系数据库，包含美国马萨诸塞州波士顿一家三级学术医疗中心收治的患者的真实住院时间。**MIMIC-IV** 包含每位患者在医院期间的全面信息：实验室测量、给药、记录的生命体征等。

该数据库旨在支持医疗保健领域的各种研究。

**MIMIC-IV** 建立在 **MIMIC-III** 的成功之上，并结合了对 **MIMIC-III**的许多改进。


**MIMIC-IV** 被分成 `module` 以反映数据的来源。目前有五个模块(`module`)：


- [hosp](./modules/hosp/_index.md) - 患者医院级别的数据：实验室、微生物、电子药物管理
- [icu](./modules/icu/_index.md) - ICU 级别数据。这些是事件表，在结构上与 MIMIC-III (`chartevents` 等) 相同
- [ed](./modules/ed/_index.md) - 来自急诊科的数据
- [cxr](./modules/cxr/_index.md) - 来自 MIMIC-CXR 的查找表和元数据，允许链接到 MIMIC-IV
- [note](./modules/note/_index.md) - 去标识化的自由文本临床笔记

---

MIMIC-Note 目前尚未公开可用，其结构可能会发生变化。

---

所有数据集中的所有患者都在 [hosp](./modules/hosp/_index.md) 模块中。

然而，并非所有 ICU 患者都有 ED 数据，并非所有 ICU 患者都有 CXR，并非所有 ED 患者都有医院数据，等等。在单个数据集中，也存在不完整的表格，因为某些电子系统在过去不存在，尤其是 eMAR 系统。

每个模块的表格在相应的部分中有详细介绍。
