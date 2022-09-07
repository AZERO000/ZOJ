[TOC]

***原本觉得这些东西是没必要写的，早之前配置过，但是由于某种原因再次配置的时候出现很多玄学问题，觉得很有必要记录一下***

事先声明一下，个人写文档是为了本人以后再次配置的时候使用的，仅方便自己，若参考后有问题可与本人联系，但不喜勿喷

## alivps_ssh连接

vps无论如何都不能用ssh连接，包括flnalshell、vscode，甚至在控制台Workbench都不能连接，属实是被莫名gank了！

解决：可以先用VNC远程连接，查找ssh文件，往root/.ssh中authorized_keys公钥文件后边追加自己电脑的rsa公钥文件，然后再用finalshell或者vscode添加rsa私钥进行ssh连接。（如果依然不行，先把自己文件备份，重装系统，解决99%的问题）在重装系统时候，一定一定要确保选定的密钥对绑定了个人服务器实例，别问我在整上边掉了多久的坑！！

1. win10生成ssh公私钥命令

> ssh -keygen
>
> 常用参数：-t 		密钥类型
>
> ​				 -b		密钥长度
>
> ​			     -f		保存密钥的文件名
>
> ​				-c 		添加注释

## 配置clash配置

1. 创建Clash文件夹，下载github上clash-linux，解压之后命名位clash，运行文件......

   > mkdir /opt/clash && cd /opt/clash 
   >
   > wget https://github.com/Dreamacro/clash/releases/download/v1.10.0/clash-linux-amd64-v1.10.0.gz 
   >
   > gunzip clash-linux-amd64-v1.10.0.gz
   >
   > mv clash-linux-amd64-v1.10.0 clash
   >
   > chmod +x clash
   >
   > ./clash

2. 第一次运行时，会抛出can't find config和 can't find MMDB的错误，并初始化其文件，找到这些文件（etc/clash），并拖到clash这个文件下。

3. 添加config.yaml文件配置，直接拿现成win下边配置文件即可，然后接着./clash 运行clash，根据报错信息修改配置文件，直到可以成功运行

4. 设置系统代理（永久代理）

   > sudo vim /etc/environment  添加接下来三行代码
   >
   > export http_proxy="http://127.0.0.1:7890"   （如果不想永久代理，可以这两行临时代理）
   >
   > export https_proxy="http://127.0.0.1:7890" 
   >
   > export no_proxy="localhost, 127.0.0.1"
   >
   > unset http_proxy     （这两行表示取消临时代理）
   >
   > unset https_proxy 
   >
   >  
   >
   > sudo vim sudo        添加下边信息
   >
   > Defaults env_keep+="http_proxy https_proxy no_proxy"

5. clash自启动和后台运行

   托管给systemd来管理自启动，生成systemd配置文件

   > /etc/systemd/system/clash.service   创建配置文件，并写入下边配置脚本
   >
   > ```
   > [Unit]
   > Description=clash daemon
   > 
   > [Service]
   > Type=simple
   > User=root
   > ExecStart=/opt/clash/clash -d /etc/clash/
   > Restart=on-failure
   > 
   > [Install]
   > WantedBy=multi-user.target
   > ```
   > \# 重载服务 sudo systemctl daemon-reload 
   >
   > \# 开机启动 sudo systemctl enable clash 
   >
   > \# 启动服务 sudo systemctl start clash 
   >
   > \# 查看服务状态 sudo systemctl status clash
