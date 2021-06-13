# docker使用笔记

docker服务停止运行的时候，所有其他依赖docker的容器都会停止运行，所以必须在--restart=always

* 删除其他未启动的容器
  `docker rm $(docker ps -a -q)`

* 将容器导出为镜像
  `docker export container-id -o xxx.tar`

* 启动mysql容器
  
  `docker run --name MYSQL -p 3307:3306 -e MYSQL_ROOT_PASSWORD=Nexon8888 -d  mysql`

*	显示docker信息

	`docker info`

使用了--link或者--network后，在容器内部ping其它容器 可以 ping 其它容器的名称

docker run --rm --restart=always --name nginx  -p 8080:80 nginx

docker run -p 1337:1337 \
             --link kong:k \
             --name konga \
             -e "NODE_ENV=production" \
             pantsel/konga:0.14.1

docker run --rm --name nginx-test -p 8084:80 -v ~/Desktop/log:/var/log/nginx -d  nginx





主从复制



```
[mysqld]
log-bin=mysql-bin #开启二进制日志
server-id=1 #设置server-id
```

主机配置

GRANT REPLICATION SLAVE  ON*.* TO 'rep'@'%'IDENTIFIED BY '123456';

flush privileges; show master status;

从机配置

CHANGE MASTER TO MASTER_HOST='172.17.0.2',MASTER_USER='rep',MASTER_PASSWORD='123456',MASTER_LOG_FILE='mysql-bin.000001',MASTER_LOG_POS=588;

start slave;

show slave status \G;

















docker哨兵模式



docker run --name slave3 -p 6282:6379 -d redis





redis-cli -h 127.0.0.1 -p 6481 -a yzdx



info replication

########docker run -d --restart=always --name ha_redis_0 --net host redis --port 6480 --requirepass 'yzdx'



docker run -d --restart=always --name ha_redis_0 --net redis redis --port 6480

docker run -d --restart=always --name ha_redis_1 --net redis redis --port 6481 --replicaof 127.0.0.1 6480 

docker run -d --restart=always --name ha_redis_2 --net redis redis --port 6482 --replicaof 127.0.0.1 6480

docker run -d --restart=always --name ha_redis_3 --net redis redis --port 6483 --replicaof 127.0.0.1 6480



docker exec -d ha_redis_1 bash -c "echo 'sentinel monitor mymaster 127.0.0.1 6480 2' > /usr/local/sentinel.conf && echo 'sentinel auth-pass mymaster yzdx'>> /usr/local/sentinel.conf &&redis-sentinel /usr/local/sentinel.conf --port 26380"

docker exec -d ha_redis_2 bash -c "echo 'sentinel monitor mymaster 127.0.0.1 6480 2' > /usr/local/sentinel.conf && echo 'sentinel auth-pass mymaster yzdx'>> /usr/local/sentinel.conf &&redis-sentinel /usr/local/sentinel.conf --port 26381"

docker exec -d ha_redis_3 bash -c "echo 'sentinel monitor mymaster 127.0.0.1 6480 2' > /usr/local/sentinel.conf && echo 'sentinel auth-pass mymaster yzdx'>> /usr/local/sentinel.conf &&redis-sentinel /usr/local/sentinel.conf --port 26382"

