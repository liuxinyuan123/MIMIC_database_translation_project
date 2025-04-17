## ICU

----

The ICU module contains information collected from the clinical information system used within the ICU. Documented data includes intravenous administrations, ventilator settings, and other charted items.

ICU 模块包含从 ICU 内使用的临床信息系统中收集的信息。记录的数据包括静脉注射、呼吸机设置和其他图表项目。

The ICU module contains data sourced from the clinical information system at the BIDMC: MetaVision (iMDSoft). MetaVision tables were denormalized to create a star schema where the icustays and d_items tables link to a set of data tables all suffixed with “events”. 

ICU 模块包含来自 BIDMC 临床信息系统 MetaVision (iMDSoft) 的数据。MetaVision 表被反规范化以创建一个星型模式，其中 icustays 和 d_items 表链接到一组以“events”为后缀的数据表。

Data documented in the icu module includes intravenous and fluid inputs (**inputevents**), ingredients of the aforementioned inputs (**ingredientevents**), patient outputs (**outputevents**), procedures (**procedureevents**), information documented as a date or time (**datetimeevents**), and other charted information (**chartevents**). All events tables contain a `stay_id` column allowing identification of the associated ICU patient in icustays, and an itemid column allowing identification of the concept documented in `d_items`.

ICU 模块中记录的数据包括静脉和液体输入（**inputevents**）、上述输入的成分（**ingredientevents**）、患者输出（**outputevents**）、程序（**procedureevents**）、记录为日期或时间的信息（**datetimeevents**）以及其他图表信息（**chartevents**）。所有事件表都包含一个 `stay_id` 列，用于识别 icustays 中相关的 ICU 患者，以及一个 itemid 列，用于识别 `d_items` 中记录的概念。

### [caregiver](./caregiver.md) table
The [caregiver](./caregiver.md) table lists deidentified provider identifiers used in the ICU module.

[caregiver](./caregiver.md) 表列出了 ICU 模块中使用的去标识化提供者标识符。

### [d_items](./d_items.md)
Dimension table describing itemid. Defines concepts recorded in the events table in the ICU module.

描述 itemid 的维度表。定义了 ICU 模块中事件表中记录的概念。

### [chartevents](./chartevents.md)
Charted items occurring during the ICU stay. Contains the majority of information documented in the ICU.

ICU 停留期间发生的图表项目。包含 ICU 中记录的大部分信息。

### [datetimesevents](./datetimesevents.md)
Documented information which is in a date format (e.g. date of last dialysis).

记录为日期格式的信息（例如最后一次透析的日期）。

### [icustays](./icustays.md)
Tracking information for ICU stays including admission and discharge times.

ICU 停留的跟踪信息，包括入院和出院时间。

### [Ingredientevents](./ingredientevents.md)
Ingredients of continuous or intermittent administrations including nutritional and water content.

连续或间歇给药的成分，包括营养和水分含量。

### [Inputevents](./inputevents.md)
Information documented regarding continuous infusions or intermittent administrations.

记录的关于连续输注或间歇给药的信息。

### [outputevents](./outputevents.md)
Information regarding patient outputs including urine, drainage, and so on.

关于患者输出的信息，包括尿液、引流等。

### [procedureevents](./procedureevents.md)
Procedures documented during the ICU stay (e.g. ventilation), though not necessarily conducted within the ICU (e.g. x-ray imaging).

ICU 停留期间记录的程序（例如通气），尽管不一定在 ICU 内进行（例如 X 射线成像）。
