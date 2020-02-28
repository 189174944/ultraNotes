# docker使用笔记

docker服务停止运行的时候，所有其他依赖docker的容器都会停止运行，所以必须在--restart=always

* 删除其他未启动的容器
  `docker rm $(docker ps -a -q)`

* 将容器导出为镜像
  `docker export container-id -o xxx.tar`

* 启动mysql容器
  
  `docker run --name MYSQL -p 3307:3306 -e MYSQL_ROOT_PASSWORD=Nexon8888 -d  mysql`
