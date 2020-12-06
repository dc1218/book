# centos7 部署django环境
## 部署mysql
- 离线安装mysql
## 部署redis
- 离线安装redis
## 部署python依赖环境
- 离线安装python依赖
## 部署python
- 离线安装python


# 离线安装
- 参考：https://www.cnblogs.com/ianduin/p/7679239.html
```

//换源
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
yum makecache

yum update
yum upgrade
wget http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
yum localinstall mysql57-community-release-el7-8.noarch.rpm
yum repolist enabled | grep "mysql.*-community.*"
yum install mysql-community-server

systemctl start mysqld


systemctl enable mysqld
systemctl daemon-reload


//修改mysql默认密码

shell> mysql -u root -p
mysql> show variables like '%password%';
mysql> set global validate_password_policy=0;
mysql> set global validate_password_length=1;
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'mm123'; 
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'mm123' WITH GRANT OPTION;
mysql> FLUSH  PRIVILEGES;



```
