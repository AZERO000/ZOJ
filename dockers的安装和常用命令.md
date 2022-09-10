# Debian安装Docker

### 卸载旧版本

> ```shell
> sudo apt-get remove docker docker-engine docker.io containerd runc
> ```

### 安装 Docker Engine-Community

在新主机上首次安装Docker Engine-Community之前，需要设置Docker仓库，然后从仓库安装和更新Docker

### 设置仓库

1. 更新apt包，安装docker的apt依赖包

   > ~~~shell
   > sudo apt-get install \
   >     apt-transport-https \
   >     ca-certificates \
   >     curl \
   >     gnupg2 \
   >     software-properties-common
   > ~~~

2. 添加Docker的官方GPG密钥，验证密钥，设置稳定版仓库

   > ```shell
   > curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/debian/gpg | sudo apt-key add -
   > sudo apt-key fingerprint 0EBFCD88
   > sudo add-apt-repository \
   >    "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/debian \
   >   $(lsb_release -cs) \
   >   stable"
   > ```

### 安装Docker Engine-Community

> ```shell
> sudo apt-get update
> sudo apt-get install docker-ce docker-ce-cli containerd.io
> ```

### 卸载Docker

> ```shell
> sudo apt-get purge docker-ce
> ```


# Docker常用命令

