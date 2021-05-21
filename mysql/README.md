# 书籍

## 涂抹MySQL

显示数据库的用户信息

查看数据库的字符集信息

### 第8章: 数据库文件结构

- 错误日志文件

- 查询日志文件

  是否可以查询和动态设置慢日志阈值

  设置慢查询日志路径, 自动进行慢查询日志备份

  是否可以在系统中启用和禁用慢查询?

  慢查询分析

- 二进制日志文件

  二进制文件的定时备份与存储

### 第9章: 数据导入与导出

导出分类

- 整库
- 单表
- 多表

### 第10章: 备份与恢复

物理备份 / 逻辑备份

完整备份 / 增量备份

### 第13章: 性能调优与诊断

性能指标

- IOPS
- QPS
- TPS
- 

# 产品规划

定时进行压力测试等， 将结果进行展示

# 安装

## docker

```shell
docker pull mysql:5.7
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
docker exec -it some-mysql bash
docker logs some-mysql
```

