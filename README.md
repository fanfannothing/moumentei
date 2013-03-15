冇问题
=====

这个Rails App由**ShiningRay**为糗事百科（2011年前版本）和秘密所搭建的

> 版权所有糗事百科 [http://www.qiushibaike.com]

Dependancy
==========
* Ruby 1.8.7 
* Rails 2.3.x 
* Bundler

安装前先 bundle install

Linux开发环境搭建指南
==================

打开终端，安装RVM，前提需要有curl
   
    sudo apt-get install curl 
    bash -s stable < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
    source ~/.bash_profile
    rvm requirements   # 

根据RVM的要求安装相应的包，如git等
安装Ruby 1.8.7 或者REE

    rvm install 1.8.7
    rvm install ree
    rvm use 1.8.7 --default 
    rvm use ree --default

安装 mercurial imagemagick mysql

    sudo apt-get install mercurial imagemagick mysql-server

安装 bundler
    
    gem i bundler

克隆代码

    git clone https://github.com/qiushibaike/moumentei

初始化 项目所用包

    cd moumentei
    bundle install

然后可以进行数据库的初始化

Windows开发环境搭建指南
====================

数据库可以在 www.mysql.com 下载并安装，或者安装xampp的版本

打开 http://rubyforge.org/projects/rubyinstaller/ 

下载1.8.7的安装包并安装，安装时勾选“Add Ruby executables to your PATH”
从刚才的地址下载DevKit并解压至任意目录，如C:\DevKit
打开cmd 

    cd C:\DevKit
    ruby dk.rb init
    ruby dk.rb install

完成安装DevKit，之后的命令行从此目录的`msys.bat`启动

并为ruby安装bundler
 
    gem i bunlder


克隆 https://github.com/qiushibaike/moumentei 至工作路径

将 `vendor/libmysql.dll` 文件复制到 Ruby 安装目录下 `bin` 目录中，如 `C:/Ruby187/bin`

从 http://code.google.com/p/msysgit/ 下载 msysgit 并安装（选中“associate .sh with msys”）

在项目目录中双击运行bundle.sh，或者在msys中进入项目工作路径，初始化项目所需的gem

    cd moumentei
    bundle install

下载安装 ImageMagick http://www.imagemagick.org/script/index.php ，上传处理图片需使用

数据库初始化
==========

将 `config/database.default.yml` 复制为 `config/database.yml` 并配置 development 节的内容

如果需要创建数据库

    bundle exec rake db:setup

如果需要初始化数据库

    bundle exec rake db:schema:load

加入基本数据

    bundle exec rake db:seed

或者直接导入 `vendor/base.sql`


服务器部署
========

服务器部署针对 Ubuntu 10.04 以上版本

对于新装机器，在deploy.rb中配置服务器信息，并在项目目录中执行 sprinkle
    
    sprinkle -s config/install.rb 

可以使用HOSTS覆盖部署目标服务器的信息

    sprinkle -s config/install.rb HOSTS=192.168.2.100

在deploy.rb中配置所需的用户名和密码、仓库用户名和密码

建立部署的目标目录结构

    cap deploy:setup

创建基本配置信息

    cap deploy:cold

检出代码并运行

    cap deploy