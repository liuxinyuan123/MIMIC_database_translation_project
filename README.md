# MIMIC-IV数据库数据转化项目

## 官方MIMIC数据库的说明
官网：https://physionet.org/content/mimiciv/3.1/

### 背景介绍
 **[英文原版背景介绍](./背景介绍/MIMIC数据文档（英文版）.md)**

 **[中英文混合版背景介绍](./背景介绍/MIMIC数据文档（中英文混合版）.md)**

**[中文翻译版背景介绍](./背景介绍/MIMIC数据文档（中文版）.md)**

### 说明文档

**[英文版说明文档](./说明文档/说明文档（英文版）.md)**

**[中英文混合版说明文档](./说明文档/说明文档（中英文混合版）.md)**

**[中文版说明文档](./说明文档/说明文档（中文版）.md)**

------
### 项目介绍
这是一个基于mimic iv数据库的一个数据挖掘相关的科研项目源代码。

### 软件准备
postgresql数据库16.0版本及以上。

### 运行环境
windows 10, 64位。
windows 11, 64位。

### 源代码修改记录
[mimic-iv数据库本地安装文件](https://github.com/MIT-LCP/mimic-code/)
将将物化视图文件[concepts_postgres](mimic-code-main/mimic-iv/concepts_postgres)进行修改。

修改内容：为每一个病例添加`hadm_id`字段。
#### 涉及的文件夹有
[concepts_postgres](mimic-code-main/mimic-iv/concepts_postgres)
, 
[comorbidity](mimic-code-main/mimic-iv/concepts_postgres/comorbidity)
, 
[demographics](mimic-code-main/mimic-iv/concepts_postgres/demographics)
,
[firstday](mimic-code-main/mimic-iv/concepts_postgres/firstday)
,
[measurement](mimic-code-main/mimic-iv/concepts_postgres/measurement)
,
[medication](mimic-code-main/mimic-iv/concepts_postgres/medication)
,
[organfailure](mimic-code-main/mimic-iv/concepts_postgres/organfailure)
,
[score](mimic-code-main/mimic-iv/concepts_postgres/score)
,
[sepsis](mimic-code-main/mimic-iv/concepts_postgres/sepsis)
,
[treatment](mimic-code-main/mimic-iv/concepts_postgres/treatment)

### 软件架构
使用postgresql 17数据库，使用pgadmin进行数据库管理。

基于mimic iv数据库，打开任意的架构下进行查询。

### 安装教程

mimic-iv数据库安装教程：
https://mimic.mit.edu/docs/

mimic-iv数据库本地安装文件：
https://github.com/MIT-LCP/mimic-code/

mimic-iv数据库使用教程：
https://mimic.mit.edu/docs/iv/

mimic-iv数据库官网：
https://physionet.org/content/mimiciv/3.1/

mimic-iv申请步骤教程：
https://physionet.org/content/mimiciv/view-required-training/3.1/#1

伦理、数据使用的审批网站：
https://about.citiprogram.org/




### 使用说明

这是助力临床研究的一项 **mimic-iv数据库** 说明文档的汉化工程

### 参与贡献

刘鑫源，青岛大学医学部，山东省青岛市，医学硕士，已毕业。

白洪翔，知右传感技术（上海）有限公司，软件工程师，中国上海市。



### 通信方式
邮箱：1980304080@qq.com


### 赞助

![支付宝](支付宝.png)

#### 银行账户
* 名称：知右传感技术（上海）有限公司
* 税号：91310113MADEJ2WB6A
* 银行账号: 121954145810001
* 开户银行: 招商银行股份有限公司上海嘉定支行
