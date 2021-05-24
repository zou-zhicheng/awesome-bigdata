# 书籍

## Neo4j实战

《Neo4j实战》([英\]阿列克萨·武科蒂奇（AleksaVukotic），等)【摘要 书评 试读】- 京东图书 (jd.com)](https://item.jd.com/11911224.html)



# Docker

```shell
docker pull neo4j
# 启动
# By default, this requires you to login with neo4j/neo4j and change the password
docker run \
    --publish=7474:7474 --publish=7687:7687 \
    --volume=$HOME/neo4j/data:/data \
    neo4j
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

