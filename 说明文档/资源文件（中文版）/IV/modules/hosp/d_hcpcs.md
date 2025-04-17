

## The *d_hcpcs* table



*d_hcpcs* 表用于获取 *hcpcsevents* 表中使用的代码的人类可读定义。这些概念主要对应于医院计费，并且主要是 CPT 代码。遗憾的是，由于许可限制，并非所有代码定义都可用。

### 连接

* *hcpcsevents* on `code`

<!--

# Important considerations

-->

## 表列描述

| 名称                  | Postgres 数据类型    |
|---------------------|------------------|
| `code`              | CHAR(5) NOT NULL |
| `category`          | SMALLINT         |
| `long_description`  | TEXT             |
| `short_description` | VARCHAR(180)     |

## 详细描述

### `code`


表示唯一事件的 5 个字符代码。

### `category`


代码的广泛分类。

### `long_description`, `short_description`

为给定行列出的 `code` 的文本描述。
