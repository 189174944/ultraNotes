## mac上启动springboot项目很慢的解决方案

报错：
2020-11-10 16:06:16.159  WARN 1124 --- [  restartedMain] o.s.boot.StartupInfoLogger        : InetAddress.getLocalHost().getHostName() took 5002 milliseconds to respond. Please verify your network configuration (macOS machines may need to add entries to /etc/hosts).

解决办法：
1、打开终端，获得主机名
➜  ~ hostname
 你的主机名.local

 2、往hosts 文件添加主机名
➜  ~ vim  /private/etc/hosts  

127.0.0.1    你的主机名.local
255.255.255.255 broadcasthost
::1       你的主机名.local

3、再启动springboot项目变得飞快了。


注入配置
1,@value("${'key.a.b'}") yml和properties都有效
2.@ConfigurationProperties(prefix="key")
3.@Environment env;env.getgetProperty("key")

JPA的Entity文件快速生成
View->Tool Windos->persistence





