## centos 安装和配置

### 1. 使用ali的源

```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
yum makecache	
```


### 2. 安装 myzsh （http://ohmyz.sh/）

> sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

### 3. 安装 nodejs， npm， yarn

```
https://www.metachris.com/2017/01/how-to-install-nodejs-7-on-ubuntu-and-centos/
https://npm.taobao.org/
https://yq.aliyun.com/articles/47269
```

### 4. 安装 jdk

> https://www.digitalocean.com/community/tutorials/how-to-install-java-on-centos-and-fedora

**配置jdk**

> sudo alternatives --config java

### 5. 安装 docker 

```
dev.aliyun.com/search.html
useradd -d /home/docker -m -s /bin/bash docker
```
