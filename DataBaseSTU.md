## 基本概念 ##

  * 数据 (Data)
  * 数据模型
    * 数据结构
    * 数据操作
      * 更新 （增、删、改）
      * 检索 （查）
    * 完整性约束 （正确性、有效性、相容性）
  * 数据库管理系统 (Database Management System，简称 DBMS)
    * 数据定义语言 —— 建立新的数据库
    * 数据操作语言/查询语言 —— 对数据库中的数据进行查询和更新
    * 支持储存大量的数据，保证对数据的正确及安全使用。
    * 控制多用户的并发访问，保证并发访问不相互影响，不损坏数据。
  * 数据库系统 (Database System，简称 DBS)
    * 一般
      * My SQL by Sun
      * SQLite3
    * 商业
      * Oracle by Oracle
      * DB2 by IBM
      * IDS (Infomix Dynamic Server) by Infomix
      * ASE (Adaptive Server Enterprise) by Sybase
      * MS SQL by Microsoft
  * 数据库系统用户
    * 偶然用户 不经常访问数据库
> > > 一般是企业或组织机构的高中级管理人员
    * 一般用户 使用应用程序访问数据库
> > > 银行的职员、航空公司的机票预定工作人员、旅馆总台服务员等
    * 特殊用户 能够直接使用数据库语言直接访问和操作数据库、编制应用程序的人
> > > 包括工程师、科学家、经济学家、科学技术工作者
  * 数据库 (Database，简称 DB)
    * 层次模型 --> 层次数据库
    * 网状模型 --> 网状数据库
    * 关系模型 --> 关系数据库
    * 对象模型 --> 对象数据库

  * 关系 —— 表
    * 各列以属性开始
    * 属性是列的入口
  * 元组 —— 记录
    * 属性下面的每一行，称为一个元组
  * 键码 —— 主码、主键
    * 能唯一确定一个元组的属性（集）
  * 域 —— 数据结构
    * 属性的取值范围叫做属性的域

  * 三层结构
    * 外模式 (external schema) 用户模式
      * 数据库用户和数据库系统的接口
      * 数据库用户的数据视图 (view)
      * 数据库用户可以看见和使用的局部数据的逻辑结构和特征描述
      * 与某一应用有关的数据的逻辑表示
      * 一个数据库通常有多个外模式
      * 一个应用程序只能使用一个外模式
      * 同一外模式可为多个应用程序所使用
      * 每个用户只能开见和访问所对应的外模式中的数据，而数据库中的其他数据均不可见
      * 关系型数据库中的视图
    * 模式 (schema)
      * 是所有数据库用户的公共数据视图
      * 是数据库中全部数据结构的逻辑机构和特征的描述
      * 一个数据库只有一个模式
      * 模式细分为
        * 概念模式 (conceptual schema)
> > > > 可用实体-联系模型来描述
        * 逻辑模式 (logical schema)
> > > > 以某种数据模型（比如关系模型）为基础，综合考虑用户的需求，并将其形成全局逻辑结构
      * 既要描述数据的逻辑结构，又要描述书记之间的联系、数据的完整性和安全性
    * 内模式 (internal schema)
      * 又称 存储模式 (storage schema)
      * 是数据库物理结构和存储方式的描述
      * 是数据在数据库内部的表示方式
      * 一个数据库只有一个内模式
      * 内容：
        * 记录的储存方式
        * 索引的组织方式
        * 数据是否压缩
        * 数据是否加密
        * 。。。
      * 不涉及物理记录
      * 不涉及硬件设备
    * 关系：
      * 模式 是数据库的核心与关键
      * 外模式通常是模式的子集
      * 内模式依赖与全局逻辑结构，但可以独立于具体的储存设备
      * 数据按外模式的描述提供给用户，按内模式的描述存储在硬盘上
      * 介于外、内模式之间
        * 不涉及外部的访问
        * 不涉及内部的存储
        * 起隔离作用，保持数据的独立性
  * 两层映像
    * 映像 (mapping):

> > 一种对应规则，说明映像双方如何进行转换
    * 外模式/模式 映像
> > 应用程序和总体逻辑关系的对应关系
      * 一个模式与多个外模式对应
      * 每个外模式都有一个外模式/模式映像用于描述该外模式与模式之间的关系
      * 外模式/模式映像通常放在外模式中描述
      * 模式改变时，改变外模式/模式映像，应用程序保持不变，为数据的逻辑独立性
    * 模式/内模式 映像
> > 总体逻辑关系和物理结构的对应关系
      * 模式只有一个
      * 内模式只有一个
      * 模式/内模式映像只有一个
      * 通常放在内模式中描述
      * 内模式改变时，改变模式/内模式映像，模式保持不变，为数据的物理独立性
    * 目的：
      * 在内模式发生变化，甚至模式发生变化时，都可以使外模式在最大程度上保持不变
      * 保证了应用程序的稳定性

  * 建模
    * ODL
    * E-R图

## 数据库语言 SQL ##

  * SQL 结构化查询语言 (Structured Query Language) "sequel"
  * SQL-86 SQL1
    * ANSI (American National Standard Institute —— 美国国家标准协会)
  * SQL-92 SQL2
  * SQL3

  * 数据查询 (data query)
  * 数据操作 (data manipulation)
  * 数据定义 (data definition)
  * 数据控制 (data control)

  * 简单查询
```
SELECT *
FROM 关系名
WHERE 选择条件
```

## 暂停 ##

  * 讲到 什么 笛卡儿积 就开始听天书了。。。
  * 还是要先补数学啊～～头大