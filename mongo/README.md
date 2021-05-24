# 书籍

## MongoDB入门经典

[《MongoDB入门经典(异步图书出品)》([美\]布拉德·戴利（Brad Dayley）)【摘要 书评 试读】- 京东图书 (jd.com)](https://item.jd.com/11702976.html)

### 第1章: NoSQL和MongoDB简介

数据对象被存储为集合中的文档, 而不是关系型数据库中的行和列。

文档是以二进制JSON(BJSON)对象的方式存储的

集合 类似于 表

### 第3章: 在MongoDB shell中使用JavaScript

### 第4章: 配置用户账户和访问控制

创建用户

add_users.js

### 第10章: 在Java应用程序中实现mongodb

### 第16章: 在Python应用程序中实现mongodb



# 资料

## [MongoDB中文网](https://www.mongodb.org.cn/)

# 命令行

```shell
# shell中输入mongo进入命令行
# 创建数据库
# 选择

```

# MongoDB中文网教程

[MongoDB教程](https://www.mongodb.org.cn/tutorial/)

## 简介

概念解析

| SQL术语/概念 | MongoDB术语/概念 | 解释/说明                           |
| :----------- | :--------------- | :---------------------------------- |
| database     | database         | 数据库                              |
| table        | collection       | 数据库表/集合                       |
| row          | document         | 数据记录行/文档                     |
| column       | field            | 数据字段/域                         |
| index        | index            | 索引                                |
| table joins  |                  | 表连接,MongoDB不支持                |
| primary key  | primary key      | 主键,MongoDB自动将_id字段设置为主键 |

数据库服务和客户端

|               |        |
| :-----------: | ------ |
| Mysqld/Oracle | mongod |
| mysql/sqlplus | mongo  |



## 数据增删

### 创建数据库

```shell
# 普通登录
# mongo
# 用账号密码登录
# mongo -u admin -p admin

# "show dbs" 命令可以显示所有数据的列表
> show dbs
# 执行 "db" 命令可以显示当前数据库对象或集合。
> db
test
# 执行 "db" 命令可以显示当前数据库对象或集合。
> use test
switched to db test
# MongoDB 创建数据库的语法格式如下：use DATABASE_NAME
# 如果数据库不存在，则创建数据库，否则切换到指定数据库。
> use mongo
switched to db mongov
```

### 删除数据库

```shell
# 刚创建的数据库 mongo 并不在数据库的列表中， 要显示它，我们需要向 mongo 数据库插入一些数据。
> db.mongo.insert({"name":"mongodb中文网"})
WriteCommandError({
	"ok" : 0,
	"errmsg" : "command insert requires authentication",
	"code" : 13,
	"codeName" : "Unauthorized"
})

> db.mongo.insert({"name":"mongodb中文网"})
WriteResult({ "nInserted" : 1 })
# 再次查看
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
mongo   0.000GB

# 删除当前数据库, 默认为test
> db.dropDatabase()
{ "ok" : 1 }

# 删除集合
> db.collection.drop()
false
```

### 插入文档

```shell
# 使用insert插入文档
# db.COLLECTION_NAME.insert(document)  
# col 是我们的集合名，前一章节我们已经创建过了，如果该集合不在该数据库中， MongoDB 会自动创建该集合并插入文档
> db.col.insert({title: 'MongoDB 教程',
... description: 'MongoDB 是一个 Nosql 数据库',
... by: 'MongoDB中文网',
... url: 'http://www.mongodb.org.cn',
... tags: ['mongodb', 'database', 'NoSQL'],
... likes: 100
... })
WriteResult({ "nInserted" : 1 })

> db.col.insert({title: 'MySQL 教程',
... ... description: 'MySQL 是一个 关系型数据库',
... ... by: 'MySQL中文网',
... ... url: 'http://www.mysql.com',
... ... tags: ['mysql', 'database', 'rdbms'],
... ... likes: 999
... ... })
WriteResult({ "nInserted" : 1 })
# 查看已插入文档
> db.col.find()
{ "_id" : ObjectId("60a78283b36f8179ba12c4c9"), "title" : "MongoDB 教程", "description" : "MongoDB 是一个 Nosql 数据库", "by" : "MongoDB中文网", "url" : "http://www.mongodb.org.cn", "tags" : [ "mongodb", "database", "NoSQL" ], "likes" : 100 }
{ "_id" : ObjectId("60a78322b36f8179ba12c4ca"), "title" : "MySQL 教程", "description" : "MySQL 是一个 关系型数据库", "by" : "MySQL中文网", "url" : "http://www.mysql.com", "tags" : [ "mysql", "database", "rdbms" ], "likes" : 999 }

## 定义变量再插入
> document=({title: 'Oracle 教程',
... description: 'Oracle 是一个 关系型 数据库',
... by: 'Oracle中文网',
... url: 'http://www.oracle.com',
... tags: ['oracle', 'database'],
... likes: 1000
... });
{
	"title" : "Oracle 教程",
	"description" : "Oracle 是一个 关系型 数据库",
	"by" : "Oracle中文网",
	"url" : "http://www.oracle.com",
	"tags" : [
		"oracle",
		"database"
	],
	"likes" : 1000
}
> db.col.insert(document)
WriteResult({ "nInserted" : 1 })
```

### 更新文档

MongoDB 使用 update() 和 save() 方法来更新集合中的文档

```shell
db.collection.update(    
	<query>, 
	<update>, 
	{       
		upsert: <boolean>,   
		multi: <boolean>,  
		writeConcern: <document>
	}
)
```

```shell
> db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```

save() 方法通过传入的文档来替换已有文档

```shell
db.collection.save(    
	<document>,     
	{      
		writeConcern: <document> 
	}  
)  
```



### 删除文档

remove()函数是用来移除集合中的数据。

在执行remove()函数前先执行find()命令来判断执行的条件是否正确，这是一个比较好的习惯。

```shell
db.collection.remove(     
	<query>,     
	{       
		justOne: <boolean>,
		writeConcern: <document> 
	} 
)
```

```shell
> db.col.remove({'title':'MongoDB'})
WriteResult({ "nRemoved" : 1 })
```

如果你只想删除第一条找到的记录可以设置 justOne 为 1，如下所示：

```
>db.COLLECTION_NAME.remove(DELETION_CRITERIA,1)
```

如果你想删除所有数据，可以使用以下方式（类似常规 SQL 的 truncate 命令）：

```
>db.col.remove({})  
>db.col.find()
```

# Docker

[mongo (docker.com)](https://hub.docker.com/_/mongo)

```shell
docker pull mongo
# 启动
# docker run --name some-mongo -d mongo:tag
# docker run --name mongo -d mongo
docker run --name mongo -p 27017:27017 -v ~/dockerdata/mongo:/data/db -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=admin -d mongo
# 进入命令行
docker exec -it mongo bash
# 查看日志
docker logs mongo
# http 访问
curl http://localhost:27017/
# docker挂载本地源代码目录
# 冒号":"前面的目录是宿主机目录，后面的目录是容器内目录
docker run -it -v /data/sample:/Users/jameszou/awesome/awesome-bigdata/mongo/teach_yourself_mongodb mongo /bin/bash

# 使用账号密码登录mongo
mongo -u admin -p admin
```

