#mysql配置实时日志


##配置实时日志

MySQL 5.1修改my.cnf，在[mysqld]下添加 log=/data/mysql/query.log 

MySQL5.7修改my.cnf，在[mysqld]下添加 general_log=ON general_log_file=/data/mysql/query.log