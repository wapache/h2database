# Wapache Database

`Wapache Database`是一款基于[h2database](http://h2database.com)并融合了多个开源项目的优秀部分的内存数据库。
目前主要作用是借此协助作者熟悉h2database和其他相关项目的原理和源代码, 长远来看, 可能会朝着商用的方向去发展和完善。

## 特性

1. 是一个内存数据库
1. 自带数据缓存功能
1. 自带连接池功能
1. 自带监控统计功能
1. 自带分库分表功能
1. 自带SQL Builder, 用于实现强类型SQL开发.
1. 支持h2,pg,mysql协议, 包含前后端协议的实现(内置了h2,pg,mysql的jdbc驱动)
1. 支持pg, mysql的cli命令.
1. 支持集群(Clustering / High Availability).

## 开发规划

1. 获取pgjdbc, mysql-connector-java代码, 改造成使用sharding-jdbc里的protocol对象.
2. 获取h2代码, 
	a. jdbc部分改造成第一步得到的jdbc驱动
	b. Parser改造成druid里的sql parser, AST暂时未定好合并方案
	c. 增加mysql server端代码
	d. 连接池部分改造成使用hikariCP代码
	e. 增加druid的统计代码
	f. 增加jooq支持.
	g. 增加支持pg, mysql的cli命令.
	h. 增加分库分表功能, 基于shardingjdbc, 扩展支持fdw处理.
	i. 支持Greenplum的gpfdist和openGauss的GDS.
3. 海量数据处理方案

    wapadb作为入口, 
	oracle/pg/mysql分库分表做oltp
	gp/gauss/clickhouse做olap

	通过流复制(基于kettle实现数据清洗/kafka)实现准实时数据同步

