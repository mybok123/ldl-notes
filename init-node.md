## centOS 服务器部署node环境

init

```
ssh root@ip
```

终端显示 ： deploy@ip's password:
输入密码

进入服务器后，默认是root用户，该用户具有最高的权限

- 在服务器新建用户:

```
sudo useradd -m -d /home/kanpo -s /bin/bash -c "the kanpo user" -U kanpo
```
-d : 指定用户登陆的主目录
-m : 为用户创建用户目录

- 为用户设定密码：

```
passwd username
```
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

－ 赋予sudo权限

sudo : super user do

如果有必要使用sudu权限，请修改

```
sudo vi /etc/sudoers
```

复制root行改为username即可

```
User privilege specification
root  ALL=(ALL:ALL) ALL
aircos  ALL=(ALL:ALL) ALL
```

-  切换用户

```
su - username
```


### 安装必备软件

centos中使用yum进行软件的安装

- 安装git

```
sudo yum update
sudo yum install git
```

- 安装nginx

```
sudo yum install nginx
```

- 安装redis

```
wget http://download.redis.io/redis-stable.tar.gz
tar xvzf redis-stable.tar.gz
cd redis-stable
make
```
出现异常自行百度


### 设置工作目录

```
mkdir -p workspace/osc
cd workspace/osc
```

-p 同时指定多级目录

- 安装nvm

默认指定shell工具为bash

```
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
source ~/.bashrc
```
- 安装node版本

```
nvm install 4
nvm ls
```
- 设定默认版本

```
nvm alias default v4.4.0
```

- 查看npm版本

```
npm -v

```

如果npm版本小于2.9,
请安装大于2.9版本

```
npm i -g npm@2.9.1
```

- 安装nrm(源管理工具)

```
npm i -g nrm
```
- 测试nrm

```
nrm test

* npm ---- 1472ms
  cnpm --- 277ms
  taobao - 135ms
  edunpm - 1466ms
  eu ----- Fetch Error
  au ----- Fetch Error
  sl ----- 3199ms
  nj ----- 4143ms
  pt ----- Fetch Error

```

- 安装pm2
 
```
npm i pm2 -g
```

### 部署nodejs项目

基础操作 ：

```
git init
git clone
npm i
pm2 start
```

### 修改nginx配置文件

- 如果托管的是静态界面， 那么修改如下内容

```
ls /etc/nginx/

conf.d                  koi-utf             scgi_params
default.d               koi-win             scgi_params.default
fastcgi.conf            mime.types          uwsgi_params
fastcgi.conf.default    mime.types.default  uwsgi_params.default
fastcgi_params          nginx.conf          win-utf
fastcgi_params.default  nginx.conf.default

vi nginx.conf

server {
        listen       80;
        server_name  yourServerName;
        root         your/folder;
        index  index.html;
        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {}

        error_page 404 /404.html;
            location = /40x.html {

        }
        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
```

修改server下的server_name, root, index

server_name 是指定的服务名称，可以自行拟定
root 下是托管的静态界面(html)文件目录
index 是root路径下面的默认文件 可以指定多个值 index.html,index.htm,index.php

- 设置nginx开机自启

```
systemctl enable nginx

systemctl restart nginx
```

- 注意 ：

```
nginx 文件首行默认用户为nginx
user nginx
```

将用户修改为你创建的用户，或者root(不推荐)

```
user yourusername
```