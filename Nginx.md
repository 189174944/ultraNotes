[TOC]

#一、nginx配置的学习

### 1.Nginx的Locatoin的使用案例

>```nginx
>location /aa {
>    alias   /usr/share/nginx/html/;
>    index  index.html index.htm index.php;
>}
>```



### 2.adasd

# 


> 干净的卸载 nginx:sudo apt-get --purge autoremove nginx









# 二、Linux相关其他配置

###防火墙配置

```sh
systemctl start firewalld  # 开启防火墙 
systemctl stop firewalld   # 关闭防火墙 
systemctl status firewalld # 查看防火墙开启状态，显示running则是正在运行 
firewall-cmd --reload     #重启防火墙，永久打开端口需要reload一下 
firewall-cmd --permanent --zone=public --add-port=8888/tcp # 添加开启端口，--permanent表示永久打开，不加是临时打开重启之后失效 
firewall-cmd --list-all #查看防火墙，添加的端口也可以看到 
```





systemctl enable nginx