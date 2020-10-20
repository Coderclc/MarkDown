

# Mysql SQL

# Navicat

# Moment

# apiDoc

# Crypto

# Koa

# MQTT

# Sequelize

# POSTMAN

# Nginx 

安装nginx

配置nginx.conf

location / {
            root   C:\Users\Administrator\Desktop\Coder\cxiaobiankeji\dist;
            index  index.html index.htm;
	    error_page  404  /index.html;
        }

cd /nginx

start nginx 启动nginx

nginx -s stop 停止nginx

空出80端口    匹配/ 转发到2333 首页    /xb 转发到3000 后台服务器

# Xshell 6

安装Xshell 6 

host: 120.25.210.169

port:22

user :root

secret key: id_rsa

# Ubuntu / Linux   

Ubuntu  linux 的发行版

apt advance package tool     sudo  superuser do

sudo apt-get install nginx  安装nginx

service nginx start/stop/reload

PORT=8081 npm start  以这个端口运行项目 

sudo apt-get install mysql-server   

sudo apt install mysql-client

sudo apt install libmysqlclient-dev

克隆代码到远程服务器->安装mysql  -> 开放远程连接->运行sql->nginx转发

## instruct

ls /  列出根的所有目录  -a 全部包括隐藏  -d  目录  -l 长数据串

clear  清屏

cd .. /home

pwd 显示当前路径  print working directory

mkdir name 创建文件夹

rmdir name 删除empty文件夹   

rm  name 删除文件  rm -rf  name 删除非空文件夹

cp 复制

mv 移动   既然移动就可以用来改名

cat 由第一行开始显示文件内容

tac 最后一行开始

nl 显示row number

more  可向下翻页

less  可上下翻页

head 只看头部几行

tail 只看尾部几行

man cp 查看cp使用说明

# WinSCP

高级验证转换secret key ppk

替换/var/www/html

# mqtt.js

client

# mosca.js

server

# PM2

node process manage

--node-args='--harmony'  启用所有harmony模块功能 就可以使用所有es6新特性

pm2 start/stop server.js    pm2 stop all   pm2 delete  name/id    pm2 restart/reload  name/id

pm2 status/list  进程

pm2 log 日志

pm2 describe name/id     view details

pm2 monit name/id    查看资源消耗

# MQTTX

simulation mqtt pubilc subscribe

因为设备发的topic 为 440000/440400/HeartBeat 

payload为 100c52b7a305c50b,48,V-0.0.31,1012 二进制buffer值<Buffer 31 30 30 63 35 32 62 37 61 33 30 35 63 35 30 62 2c 34 38 2c 56 2d 30 2e 30 2e 33 31 2c 31 30 31 32 30>,

server,同时也是mqtt client,要先连接时订阅subscribe才能在 client.on message monitor

所以设备发的topic要在mosca 处理 ,因为所有的publish,都会被mosca 的server.on published捕获

# Redis

Remote Dictionary Server

高性能的key-value数据库。

开启服务器 redis-server

连接服务器 redis-cli -h localhost -p 6379

设置键值对  set key value

get key

# Ioredis

# YARN

# Git

```sh
git clone https://用户:密码@git.coding.net/git/repo.git
```

# PM2LOGROTATE

pm2 install pm2-logrotate

**NOTE:** the command is `pm2 install` NOT `npm install`

max_size（默认为10M）：当文件大小大于此值时，它将旋转该文件（可能是在文件实际超过限制后，工作人员检查该文件）。您可以指定结束时的单位：10G、10M、10K

retain（默认为30个文件日志）：这个数字是一次保存的循环日志数，这意味着如果retain=7，则最多将有7个旋转日志和当前日志。

compress（默认为false）：通过gzip为所有旋转的日志启用压缩

dateFormat（默认为YYYY-MM-DD U HH-MM-ss）：使用日志文件名称的数据格式

rotateModule（默认为true）：像其他应用程序一样旋转pm2模块的日志

workerInterval（默认为30秒）：您可以控制worker检查日志大小的间隔（最小值为1）

rotateInterval（默认值为0 0***每天午夜）：此cron用于在执行时强制旋转。我们使用节点调度来调度cron，因此节点调度的所有有效cron都是这个选项的有效cron。Cron样式：

TZ（默认为系统时间）：这是标准的TZ数据库时区，用于偏移保存的日志文件。例如，一个值为Etc/GMT+1（每小时一个日志）将在格林尼治时间14时保存一个文件，日志名为13小时（GMT+1）。

pm2 set pm2-logrotate:<param> <value>

```
pm2 set pm2-logrotate:max_size 10M
pm2 set pm2-logrotate:workerInterval 3600
pm2 set pm2-logrotate:retain 30
pm2 set pm2-logrotate:dateFormat YYYY-MM-DD__HH-mm-ss
pm2 set pm2-logrotate:TZ Asia/Shanghai
```

