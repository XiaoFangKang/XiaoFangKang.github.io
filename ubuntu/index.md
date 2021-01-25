# Docker 安装


# Ubuntu Docker 安装
## 使用官方安装脚本自动安装
### 安装命令如下：

```shell
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

### 也可以使用国内 `daocloud` 一键安装命令：

```shell
curl -sSL https://get.daocloud.io/docker | sh
```





# Docker 镜像加速
国内从 `DockerHub` 拉取镜像有时会遇到困难，此时可以配置镜像加速器。`Docker` 官方和国内很多云服务商都提供了国内加速器服务，例如：

科大镜像：`https://docker.mirrors.ustc.edu.cn/`
网易：`https://hub-mirror.c.163.com/`
阿里云：`https://<你的ID>.mirror.aliyuncs.com`
七牛云加速器：`https://reg-mirror.qiniu.com`
