# MIMIC-IV数据库汉化项目

## 项目背景
这是助力临床研究的一项 **mimic-iv数据库** 说明文档的汉化工程。

**请注意：** 当你看到这篇文档时，我们默认你懂得如何申请和使用mimic数据库，并且已经在正规渠道获得mimic数据库使用权限，并获得CIIT官方认证。如果不知如何申请，可通过本文件下方的官网进行检索，如有问题可联系我们。

**本项目不会为你解决任何关于官方认证、伦理认证的问题，包括官网题目的答案我们将不会提供。**

------

### MIMIC数据库介绍介绍

MIMIC全称是Medical Information Mart for Intensive Care, 是一个重症医学数据库。2003年，在NIH的资助下，来自贝斯以色列女执事医疗中心(Beth Israel Deaconess Medical Center)、麻省理工(MIT)、牛津大学和麻省总医院(MGH)的急诊科医生、重症科医生、计算机科学专家等共同建立的一个数据库。 

目前很多科研项目都用到了mimic数据库，但由于英文原版的说明文档阅读起来极不友好，因此，我们决定将mimic数据库的英文版说明文档进行汉化。

汉化的内容包括：
* 英文版说明文档汉化。
* 说明文档汉化。
* ICD 版本汉化。

我们提供了3种说明文档，分别对应2种语言，提供中文版、英文版、中文英文对照版。

------

## 参与人员
* 刘鑫源，青岛大学医学部，医学硕士，青岛市，山东省，中国。

* 白洪翔，知右传感技术（上海）有限公司，软件工程师，上海市，中国。


## 通信方式
如需协助mimic数据库的安装（windows系统）、数据提取的sql语句，可联系以下邮件。

邮箱：17386506353@189.cn

------

## 官方MIMIC数据库的说明
官网：https://physionet.org/content/mimiciv/3.1/

### 背景介绍
*  **[英文原版背景介绍](./背景介绍/MIMIC数据文档（英文版）.md)**
*  **[中英文混合版背景介绍](./背景介绍/MIMIC数据文档（中英文混合版）.md)**
* **[中文翻译版背景介绍](./背景介绍/MIMIC数据文档（中文版）.md)**

----

### 说明文档

* **[英文版说明文档](./说明文档/说明文档（英文版）.md)**
* **[中英文混合版说明文档](./说明文档/说明文档（中英文混合版）.md)**
* **[中文版说明文档](./说明文档/说明文档（中文版）.md)**

------

## ICD 诊断代码手册汉化

>《疾病和有关健康问题的国际统计分类》（International Statistical Classification of Diseases and Related Health Problems，简称《国际疾病分类》（International Classification of Diseases，ICD），是全世界通用的疾病分类系统和诊断工具，适用于流行病学、卫生服务管理及临床实践。ICD由世界卫生组织负责维护。ICD最初是设计成医疗保健分类系统，提供整套诊断代码来分类疾病，细项分类涵盖各种征象、症状、异常发现、民众投诉、社会环境、以及疾病或伤害的外部原因。此系统的用意是绘制健康条件的知识地图，既能对应通用类别，也能归于特定变化，并为之分配一个指定代码，长度最多为六个字符。准此，主要类别通常会包括一整组相似的疾病。

ICD诊断代码在mimic数据库中有2个版本，分别为 **ICD-9** 和 **ICD-10**。

本项目中提供ICD版本的汉化，提供了2个版本，分别为：

* **[ICD-9 版本中英对照汉化版](./ICD对照手册/ICD诊断代码对照手册/ICD9/index.md)**
* **[ICD-10 版本中英对照汉化版](ICD对照手册/ICD诊断代码对照手册/ICD10/_index.md)**

> 注意：因Gitee里面不支持过大的markdown文件的网页显示，因此本项目提供分段的ICD编码手册。

-----

## ICD操作代码

* **[ICD-9 操作代码汉化版](./ICD对照手册/ICD操作代码对照手册/ICD9/ICD-9-CM.md)**
* **[ICD - 10 操作代码中英对照汉化版](./ICD对照手册/ICD操作代码对照手册/ICD10/_index.md)**

> 注意：因Gitee里面不支持过大的markdown文件的网页显示，因此本项目提供分段的ICD编码手册。


-----

## 化验检查ID对照字典
* **[化验检查ID对照字典中英对照版](./化验检查ID对照字典/化验检查ID对照字典汉化版.md)**

-----

## 项目介绍
这是一个基于mimic iv数据库的一个数据挖掘相关的科研项目源代码。

------

## 软件准备
postgresql数据库16.0版本及以上。

[postgresql官网下载](https://www.postgresql.org/download/)

https://www.postgresql.org/download/

------

## 运行环境
windows 10, 64位。
windows 11, 64位。

------

## 安装教程

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

如需要安装数据库的协助，可以通过本文件下面的联系方式与本团队获得联系。

------

### 软件架构及软件准备
使用postgresql 17数据库管理。

本工程修改后的代码进行安装结束后，可在navicat、pgadmin、datagrip等主流数据库查询软件中进行数据库查询。

------

### 参与人员贡献与利益冲突声明

刘鑫源，青岛大学医学部，山东省青岛市，医学硕士，已毕业。

白洪翔，知右传感技术（上海）有限公司，软件工程师，中国上海市。

无经济与利益冲突。

## 通信方式
如需协助mimic数据库的安装（windows系统）、数据提取的sql语句，可联系以下邮件。

邮箱：17386506353@189.cn

## 交流互动

### **[QQ群：934942955](https://qm.qq.com/q/hIJs3oWeis)**
![QQ群.jpg](%E4%BA%92%E5%8A%A8%E4%BA%A4%E6%B5%81/QQ%E7%BE%A4.jpg)

### [需求收集文档](https://docs.qq.com/aio/DSEJaZHRyUU1zZklI)

【腾讯文档】需求文档 https://docs.qq.com/aio/DSEJaZHRyUU1zZklI

![需求文档二维码.png](%E4%BA%92%E5%8A%A8%E4%BA%A4%E6%B5%81/%E9%9C%80%E6%B1%82%E6%96%87%E6%A1%A3%E4%BA%8C%E7%BB%B4%E7%A0%81.png)



## 捐赠

支持项目开发，可通过以下方式进行捐赠。您的支持是我们继续下去的动力！

### 支付宝
![支付宝.png](%E4%BA%92%E5%8A%A8%E4%BA%A4%E6%B5%81/%E6%94%AF%E4%BB%98%E5%AE%9D.png)

### 银行账户
* 名称：知右传感技术（上海）有限公司
* 税号：91310113MADEJ2WB6A
* 银行账号: 121954145810001
* 开户银行: 招商银行股份有限公司上海嘉定支行
