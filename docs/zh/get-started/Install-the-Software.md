# 安装IRIShub

## 服务器配置要求


首先，你需要配置一台服务器。你的验证人节点应该能够一直运行，所以你可能需要在一台数据中心的服务器。任何像AWS、GCP、DigitalOcean中的云服务器都是适合的。

IRIS Hub是用Go语言编写的。它可以在任何能够编译并运行Go语言程序的平台上工作。然而，我强烈建议在Linux服务器上运行验证人节点。我曾经尝试在Windows上运行验证人节点。我能够顺利的编译但是在运行的时候会有一些问题。接下来的说明和指导都是基于Linux服务器的。
这是我们推荐的服务器的配置：

* CPU核数：2
* 内存容量：6GB
* 磁盘空间：256GB SSD
* 操作系统：Ubuntu 18.04 LTS/16.04 LTS
* 带宽: 20Mbps
* 允许的入方向的链接：TCP端口 26656 和 26657


#### 方法1：下载发行版安装

进入下载页: https://github.com/irisnet/irishub/releases/
下载对应版本的可执行文件
解压缩
```
unzip iris$VERSION.$OS-$ARCH.zip -d /usr/local/bin/
```
拷贝到/usr/local/bin/目录下 
执行以下命令,若出现对应的版本号则说明安装成功。

```
$ iris version
v0.12.3
    
$ iriscli version
v0.12.3
```
#### 方法2：源码编译安装

#### 安装Go版本 1.11+ 


系统要求：

Ubuntu LTS 16.04


安装IRIShub需要保证Go的版本在1.11以上，

通过执行以下命令安装1.11版本的Go。

```
$ sudo add-apt-repository ppa:gophers/archive
$ sudo apt-get update
$ sudo apt-get install golang-1.11-go
```

以上命令将安装 golang-1.11-go在 /usr/lib/go-1.11/bin. 需要将它加入到PATH中

```
echo "export PATH=$PATH:/usr/lib/go-1.11/bin" >> ~/.bash_profile
source ~/.bash_profile
```

同时，你需要指定相关的 $GOPATH, $GOBIN, 和 $PATH 变量, 例如:

```
mkdir -p $HOME/go/bin
echo "export GOPATH=$HOME/go" >> ~/.bash_profile
source ~/.bash_profile
echo "export GOBIN=$GOPATH/bin" >> ~/.bash_profile
source ~/.bash_profile
echo "export PATH=$PATH:$GOBIN" >> ~/.bash_profile
source ~/.bash_profile
```

参考链接：

1. https://golang.org/doc/install
2. https://github.com/golang/go/wiki/Ubuntu



#### 下载源码并安装


在完成Go的安装后，通过以下命令下载并安装IRIS hub相关程序.

* 编译用于`测试网`的可执行文件:

```
mkdir -p $GOPATH/src/github.com/irisnet
cd $GOPATH/src/github.com/irisnet
git clone https://github.com/irisnet/irishub
cd irishub && git checkout v0.12.3
curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
source scripts/setTestEnv.sh
make all
```

* 编译用于`betanet`的可执行文件:
```
mkdir -p $GOPATH/src/github.com/irisnet
cd $GOPATH/src/github.com/irisnet
git clone https://github.com/irisnet/irishub
cd irishub && git checkout v0.12.3
curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
make all
```

以上命令将完成iris 和 iriscli的安装. 若出现对应的版本号则说明安装成功。

```
$ iris version
v0.12.3
    
$ iriscli version
v0.12.3
```
### 如何升级IRIShub

通过执行一下命令可以完成测试网上IRIShub从v0.12.0到v0.12.1的升级

```
iris unsafe-reset-all --home
cd $GOPATH/src/github.com/irisnet/irishub
git fetch -a origin
git checkout v0.12.3
make all
```
