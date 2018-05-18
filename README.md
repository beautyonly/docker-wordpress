# WPDC - Wordpress Docker 使用文档

####  使用Docker和Docker Compose进行Easy Wordpress开发Compose

## 开始一个新项目

确保你的机器上安装了最新版本的Docker和Docker Compose。将docker-compose.yml文件从此存储库复制到空白文件夹中。

在该文件中，您可以更改IP地址（如果您运行多个容器）或将数据库从mysql更改为mariadb。

##### 创建容器

打开一个终端并cd到你有docker-compose.yml的文件夹并运行:
```
sudo docker-compose up
```

这会在docker-compose.yml文件旁边创建2个新文件夹.
* **wp-data** - 用于存储和恢复数据库转储 

* **wp-app** - 您的Wordpress应用程序的位置

这些容器现在正在构建和运行。您应该能够使用浏览器地址中的配置IP访问Wordpress安装。为了方便起见，您可以在主机文件中添加一个新条目

##### 启动容器
您可以使用守护进程模式下的up命令（通过将-d添加为参数）或使用start命令启动容器
```
sudo docker-compose start
```

##### 停止容器
```
sudo docker-compose stop
```

##### 取出容器
要停止并删除所有容器，请使用down命令
```
sudo docker-compose down
```
... 或者rm命令，如果容器已经停止
```
sudo docker-compose rm
```

## 存储自己现在有的wordpress文件与数据库代码文件

将docker-compose.yml文件复制到一个新目录中。在目录中创建两个文件夹：
* **wp-data** - 数据库存储位置
* **wp-app** - 复制现有的wordpress代码到这个目录

您现在可以使用up命令;
```
sudo docker-compose up
```
这将创建容器并使用给定的转储填充数据库。您可以设置您的主机条目并将其更改到数据库中，或者您只需在wp-config.php中通过添加
```
define('WP_HOME','http://wp-app.local');
define('WP_SITEURL','http://wp-app.local');
```

## 创建数据库转储
```
sudo ./export.sh
```
---

## 使用一个主题修改位置

配置卷以在docker-compose.yml的容器中加载主题
```
volumes:
  - ./theme-name/trunk/:/var/www/html/wp-content/themes/theme-name
```

## 使用插件目录

配置卷以在docker-compose.yml中的容器中加载插件

```
volumes:
  - ./plugin-name/trunk/:/var/www/html/wp-content/plugins/plugin-name
```
