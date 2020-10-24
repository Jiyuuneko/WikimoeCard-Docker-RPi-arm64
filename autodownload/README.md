# 自动下载程序源码

本Docker不用手动下载源码复制到文件夹，手动修改版本号下载对应版本。

Due to the direct download from Github, the download speed may be slow if you are in mainland China.

修改 `dockerfile` 文件内的版本号码对应最新的版本:

```
ENV WC_VERSION 2.9.8
```

构建Docker执行下面的命令:

```
docker build -t wikimoecard:latest .
```
