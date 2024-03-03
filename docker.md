> 部分内容源自AI

0. 更新源（neo-pi需要arm64，同时考虑魔法）：
````
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial main multiverse restricted universe 
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-backports main multiverse restricted universe 
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-proposed main multiverse restricted universe 
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-security main multiverse restricted universe 
deb http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-updates main multiverse restricted universe 
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial main multiverse restricted universe 
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-backports main multiverse restricted universe 
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-proposed main multiverse restricted universe 
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-security main multiverse restricted universe 
deb-src http://mirrors.ustc.edu.cn/ubuntu-ports/ xenial-updates main multiverse restricted universe
````
1. 更新软件包列表
首先，打开终端并更新你的软件包列表以确保所有包都是最新的：
````
sudo apt update
sudo apt upgrade -y
````
2. 安装依赖包
安装一些必要的包，这些包允许 apt 通过 HTTPS 使用仓库：
````
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
````
3. 添加 Docker 的官方 GPG 密钥
````
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
````
4. 设置 Docker 仓库
对于 ARM64 架构，你需要确保添加的仓库支持你的架构。添加 Docker 仓库之前，使用 lsb_release -cs 确认你的 Ubuntu 版本代号，然后添加仓库：
````
sudo add-apt-repository "deb [arch=arm64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) test"
````
5. 安装 Docker CE
更新 apt 包索引，并安装 Docker CE（社区版）：
````
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
````
6. 验证安装
安装完成后，检查 Docker 是否成功安装并运行：
````
sudo systemctl status docker
````
或者运行一个测试容器：
````
sudo docker run hello-world
````
7. 启用 Docker 服务的自动启动
打开终端，执行以下命令来启用 Docker 服务的自动启动：
````
sudo systemctl enable docker
````
这个命令会创建一个符号链接，将 Docker 服务的配置文件链接到系统的启动目录中，从而在系统启动时自动启动 Docker 服务。
