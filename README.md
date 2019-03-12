# 论文投稿系统

​	本论文投稿系统是通过[websubrev](https://shaih.github.io/websubrev/)(版本号0.64)，重新修改而成,原系统只在PHP4.3.9和MySQL4.1.20进行测试过，而对于目前的系统几乎不适用了。所以在我使用该系统过程中进行了适当的修改，使其能够正常运行在当前的LINUX系统环境当中，希望本系统能够对你有所帮助。

# 运行环境

- Ubuntu16.04
- PHP7.2
- MySQL5.7.25
- Apache2

# 安装步骤

MySQL：

​	sudo apt-get install mysql-server

​	sudo apt install mysql-client

​	sudo apt install libmysqlclient-dev

​	在MySQL里输入命

​	SET GLOBAL sql_mode ='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';令

PHP：

​	sudo apt install php

​	sudo apt-get install libapache2-mod-php

​	sudo apt-get install php7.2-fpm php7.2-mysql php7.2-common

将php.ini的 sendmail_path = "/usr/bin/msmtp -t "

Apache2:

​	sudo apt install apache2	

MSMTP：

​	sudo apt-get install msmtp msmtp-mta ca-certificates

​	配置：vim /etc/msmtprc 

​		account 163

​		tls on

​		tls_certcheck off

​		tls_starttls off

​		host smtp.163.com

​		port 465

​		auth login

​		user xxxx@163.com

​		password 密码

​		from xxxx@163.com

​		logfile /var/log/msmtp/msmtp.log

​		account default : 163

​	测试：

​	echo "Subject:测试"|msmtp -d xxx@xx.com	

解压文件包放到/var/www/html目录下

将webtree提取出来

然后chmod o+w init subs chair

# 使用步骤

主席端：http://192.168.100.22/webtree/chair

委员端：http://192.168.100.22/webtree/review（要使用委员端要注意主席端先将提交的日期关闭后才能让委员去评审论文）

提交者端：http://192.168.100.22/webtree/submit

# 错误问题

1. PHP Fatal error:  Uncaught PDOException: SQLSTATE[HY000] [1698] Access denied for user 'root'@'localhost'

   解决方案：update mysql.user set authentication_string=PASSWORD('111111'),plugin='mysql_native_password' where user='root';

   重启mysql、apache2

2. 无法显示phpinfo

   将php.ini的short_open_tag=ON