
## *provider*


由 *provider_id* 引用的数据库中提供治疗操作等的描述表。
从 MIMIC-IV v2.2 开始，此表仅列出数据库中所有唯一的 `provider_id`。

Note that most tables contain a prefix before `provider_id`. All columns with a suffix link to `provider_id`, including:

请注意，大多数 table 在 'provider_id' 之前都包含前缀。带有后缀链接到 'provider_id' 的所有列，包括：

* `admit_provider_id`
* `enter_provider_id`
* `order_provider_id`

## 表列

| Name        | Postgres data type   |
|-------------|----------------------|
| provider_id | VARCHAR(10) NOT NULL |

### `provider_id`


`provider_id` 列出了整个数据库中使用的提供程序的所有可能标识符。
