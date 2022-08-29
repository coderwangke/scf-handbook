# SLS Cli方式实现多namespace发布

背景：客户走 [SLS Cli](https://cloud.tencent.com/document/product/583/44751) 方式部署应用时，会部署到多个环境（比如正式和测试）。而 serverless 平台当前是以 namespace 方式做隔离，所以需要客户做多 namespace 的应用发布。
接下来介绍下具体的配置方案

## `.env` 文件方式

`.env` 文件样例：

```shell
# .env 文件

STAGE=prod
NAMESPACE=default # 修改NAMESPACE的值实现不同的命名空间发布
NAME=test
```

serverless.yml 文件样例：
```shell
# serverless.yml
app: helloworld
stage: ${env:STAGE} # stage 默认值：stage=dev

component: scf
name: ${env:NAME}

inputs:
name: ${app}-${name}-${stage}
src: ./
description: golang 空白模板函数
type: event
handler: main
runtime: Go1
namespace: ${env:NAMESPACE}
region: ap-guangzhou
memorySize: 128
timeout: 3
environment: #  环境变量
variables: #  环境变量对象
Lang: golang
```

补充：

● serverless cli 部署应用时，唯一标识字段是：app / stage / name

● SCF控制台上看的应用名是：inputs.name

● 建议做namespace隔离时，附以 stage 做结合

## 命令行方式
参考如下：

1、 部署函数

```shell
# 指定 stage
sls deploy --stage=prod
# 指定 函数的命名空间
sls deploy --inputs namespace=dev
# 设置 环境变量
sls deploy --inputs namespace=dev environment='{"variables": {"stage": "dev"}}'
```

2、删除函数

```shell
# 删除
# 指定 stage
sls deploy --stage=prod
```



