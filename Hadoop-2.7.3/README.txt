hadoop集群

账户
root / QQ24057399
admin	/ QQ240573990

192.168.114.10 master
192.168.114.11 slave1
192.168.114.12 slave2


ssh-copy-id root@master
ssh-copy-id root@slave1
ssh-copy-id root@slave2

ssh master date
ssh slave1 date
ssh slave2 date

nmtui  网络编辑窗




vim  进入文件
/【查询内容】  回车键 确认
n 下一个



export HADOOP_HOME=/usr/hadoop-2.7.3/
export PATH=$PATH:$HADOOP_HOME/bin



查看本机启动的所有端口：netstat -nultp
抓取进程：ps -ef|grep [名称]  如：ps -ef|grep hadoop 

杀死进程：kill -9 进程号  

停止防火墙服务：systemctl stop firewalld
禁用防火墙，下次开机启动后防火墙服务不再启动：systemctl disable firewalld

重新连接网络：systemctl restart network

立即关闭：shutdown -h now

立即重启：reboot   =  shutdown -r now


查看hadooop进程启动情况：ps -ef|grep hadoop 

一、Centos7登陆：1、root QQ240573990 / 2、admin QQ240573990
二、启动Hadoop：1、cd /usr/hadoop-2.7.3/sbin  2、./start-all.sh（只在master）
三、登陆mysql：1、mysql -u root -p  2、QQ240573990（只在master）
四、启动hive:1、/opt/apache-hive-1.2.2-bin/bin    2、./schematool -dbType mysql -initSchema      3、hive（只在master）
五、启动Zookeeper：1、zkServer.sh start（所有）  2、zkServer.sh stop  3、验证 jps
六、启动Hbase：1、cd /opt/hbase-1.2.6/bin 2、start-hbase.sh（只在master） 3、验证：hbase shell  3、list 4、stop-hbase.sh
	系统重启可能会删除 /opt/hbase-1.2.6/pids
七、启动Sqoop：1、sqoop help（只在master）



--connect  配置数据库连接为MySQL中数据库
--driver 驱动
--table 表名
--username mysql用户名
--password mysql密码
--target-dir 导入hdfs指定目录
--m 表示Mapper数量
sqoop import \
--connect jdbc:mysql://localhost:3306/sqoop_hive \
--driver com.mysql.jdbc.Driver \
--table orders \
--username root \
--password root \
--target-dir /data/retail_db/orders \
--m 3

执行sh文件无权限，给文件目录增加权限，如：/opt/**.sh  chmod -R 775 opt


linux mysql 创建对外访问用户，并赋予权限
1.第一步是刷新MySql的权限：flush privileges;
2.添加一个允许给外网访问的用户：create user 'zhu'@'%' identified by '123456';
3.对创建的用户进行授权：grant all privileges on *.* to 'zhu'@'%' identified by '123456';
4.再执行一遍权限刷新：flush privileges;

#显示当前运行
ps -aux
#这个更简练
ps -aut

#杀掉PID
kill -9 PID

wget https://pkg.jenkins.io/redhat/jenkins-2.222.3-1.1.noarch.rpm
