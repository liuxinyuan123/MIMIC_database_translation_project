住院期间发生的计费事件。包括 CPT 代码。


## *hcpcsevents*

## 表连接
* *d_hcpcs* on hcpcs_cd

<!--

# Important considerations

-->

## 表列描述

| Name                | Postgres data type |
|---------------------|--------------------|
| `subject_id`        | INTEGER NOT NULL   |
| `hadm_id`           | INTEGER NOT NULL   |
| `chartdate`         | DATE               |
| `hcpcs_cd`          | CHAR(5) NOT NULL   |
| `seq_num`           | INTEGER NOT NULL   |
| `short_description` | VARCHAR(180)       |

### `subject_id`
### `hadm_id`
### `chartdate`
  与编码事件相关的日期。

### `hcpcs_cd`
  一个五字符代码，唯一代表该事件。

  将此链接到 *d_hcpcs* 中的 `code` 以获取代码的更长描述。

### `seq_num`
  为个别住院分配的 HCPCS 代码顺序。此顺序有时传达含义，例如有时表示更高的优先级，但这并不能保证适用于所有代码。

### `short_description`
  对给定行中列出的 `hcpcs_cd` 的简短文本描述。
