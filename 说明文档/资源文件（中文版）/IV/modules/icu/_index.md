## ICU

----

ICU 模块包含从 ICU 内使用的临床信息系统中收集的信息。记录的数据包括静脉注射、呼吸机设置和其他图表项目。

ICU 模块包含来自 BIDMC 临床信息系统 MetaVision (iMDSoft) 的数据。MetaVision 表被反规范化以创建一个星型模式，其中 icustays 和 d_items 表链接到一组以“events”为后缀的数据表。



ICU 模块中记录的数据包括静脉和液体输入（**inputevents**）、上述输入的成分（**ingredientevents**）、患者输出（**outputevents**）、程序（**procedureevents**）、记录为日期或时间的信息（**datetimeevents**）以及其他图表信息（**chartevents**）。所有事件表都包含一个 `stay_id` 列，用于识别 icustays 中相关的 ICU 患者，以及一个 itemid 列，用于识别 `d_items` 中记录的概念。

### [caregiver](./caregiver.md) table

[caregiver](./caregiver.md) 表列出了 ICU 模块中使用的去标识化提供者标识符。

### [d_items](./d_items.md)
描述 itemid 的维度表。定义了 ICU 模块中事件表中记录的概念。

### [chartevents](./chartevents.md)
ICU 停留期间发生的图表项目。包含 ICU 中记录的大部分信息。

### [datetimesevents](./datetimesevents.md)
记录为日期格式的信息（例如最后一次透析的日期）。

### [icustays](./icustays.md)
ICU 停留的跟踪信息，包括入院和出院时间。

### [Ingredientevents](./ingredientevents.md)
连续或间歇给药的成分，包括营养和水分含量。

### [Inputevents](./inputevents.md)
记录的关于连续输注或间歇给药的信息。

### [outputevents](./outputevents.md)
关于患者输出的信息，包括尿液、引流等。

### [procedureevents](./procedureevents.md)
ICU 停留期间记录的程序（例如通气），尽管不一定在 ICU 内进行（例如 X 射线成像）。
