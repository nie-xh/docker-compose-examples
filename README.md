# docker-compose-examples文档

## 简介
提供linux和windows下docker-compose组件部署样例，帮助快速搭建开发环境。
data、conf、logs等该挂载的目录都默认挂载了，亲自做过测试，基本上可以一键构建，不需要修改docker-compose文件，个性化的配置可以在conf中修改

## 使用
根据要部署的环境，分别拷贝linux和windows下的docker文件夹到安装目录，然后进入对应的组件文件夹，执行docker-compose up -d构建容器。


## 目录结构说明
```
source
    -linux -- linux环境下部署样例
        -docker -- docker目录，部署时将该目录整体拷贝到linux下要部署的目录
            -组件 -- 组件目录
                -conf   --配置文件
                -docker-compose.yml 
    -windows -- windows环境下部署样例
        -docker -- docker目录，部署时将该目录整体拷贝到windows下要部署的目录
            -与linux下结构相同
```
windows下使用docker-compose强烈推荐docker desktop，可以很方便的一键管理自己的windows下的docker容器。成功安装并启动docker desktop后，在windows的powershell中即可使用docker相关命令。
组件安装完毕后，界面效果如下：
![](./src/img/Snipaste_2023-05-16_16-32-41.png)





## 注意
1. 每个组件对应的配置文件请在构建前按自己实际情况修改，192.168.0.154为我本机ip，请修改成自己机器ip



## Q&A
1. es构建如果报错max virtual memory areas vm.max\_map\_count \[65530\] is too low, increase to at least \[262144\]（elasticsearch用户拥有的内存权限太小，至少需要262144）

    解决：
    ~~~shell
    # 修改配置sysctl.conf
    [root@localhost ~]# vi /etc/sysctl.conf
    # 添加下面配置：
    vm.max_map_count=262144
    # 重新加载：
    [root@localhost ~]# sysctl -p
    # 最后重新启动elasticsearch，即可启动成功。
    ~~~
