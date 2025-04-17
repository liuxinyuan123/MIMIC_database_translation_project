# ED module

ED 模块包含急诊科患者在急诊科期间收集的数据。

信息包括入院原因、分诊评估、生命体征和药物核对。

`subject_id` 和 `hadm_id` 标识符允许将 MIMIC-IV-ED 与其他 MIMIC-IV 模块链接。

----

## [diagnosis](./diagnosis.md) table

*[diagnosis](./diagnosis.md)* 表提供患者的计费诊断。

诊断是在患者从急诊科出院后确定的。

## [edstays](./edstays.md) table

*[edstays](./edstays.md)* 表是急诊科就诊的主要跟踪表。

它提供了患者进入急诊科的时间和离开急诊科的时间。

## [medrecon](./medrecon.md) table

在进入急诊科时，工作人员会询问患者目前正在服用的药物。

这个过程称为药物核对，*[medrecon](./medrecon.md)* 表存储了护理人员的发现。

## [pyxis](./pyxis.md) table

*[pyxis](./pyxis.md)* 表提供了通过 Pyxis 系统进行的药物分发信息。

请注意，由于同一种药物可能有多个 `gsn` 值，因此每一行并不一定表示唯一的分发。

`med_rn` 列允许选择单个分发。

## [triage](./triage.md) table

*[triage](./triage.md)* 表包含患者在急诊科首次分诊时的信息。

患者在分诊时由一名护理人员进行评估，并询问一系列问题以评估其当前的健康状况。

测量他们的生命体征并分配一个紧急程度。

根据紧急程度，患者要么在候诊室等待稍后处理，要么优先进行即时护理。

## [vitalsign](./vitalsign.md) table

进入急诊科的患者每 1-4 小时进行一次常规生命体征测量。

这些生命体征存储在 *[vitalsign](./vitalsign.md)* 表中。