---
layout: post
title: ElasticSearch数据迁移
category: ELK
tags: [ELK]
excerpt: ElasticSearch数据迁移
keywords: ELK,数据迁移
---

# ElasticSearch数据迁移

## ElasticDump工具在Github的源码仓库

```
https://github.com/taskrabbit/elasticsearch-dump  访问该网址，可以看到详细的安装与使用流程，请先阅读该部分内容。
```

## ES集群信息

### 1、ES集群-Old的ES节点-Source
- http://10.122.12.234:9200/_plugin/head/
```
10.122.12.234
10.122.12.235
10.122.12.236
10.122.12.237
```
### 2、ES集群-New的ES节点-Target
- http://10.96.83.170:9200/_plugin/head/
```
10.96.83.170
10.96.83.171
10.96.83.179
10.96.83.182
```

## 数据迁移脚本-使用 ElasticDump

### 1、安装elasticdump

```
yum install -y epel-release
yum install -y nodejs
yum install -y npm
npm install elasticdump
```

### 2、切换到elasticdump目录     

```
cd node_modules/elasticdump/bin
```

### 3、执行数据迁移-根据实际需要迁移的数据修改IP、index等参数
    
```
首先迁移mapping和analyzer信息 
./elasticdump --ignore-errors=true  --scrollTime=120m  --bulk=true --input=http://10.122.12.234:9200/time   --output=http://10.96.83.170:9200/time  --type=analyzer   

./elasticdump --ignore-errors=true  --scrollTime=120m  --bulk=true --input=http://10.122.12.234:9200/time   --output=http://10.96.83.170:9200/time  --type=mapping  


再进行数据迁移 
./elasticdump --ignore-errors=true  --scrollTime=120m  --bulk=true --input=http://10.122.12.234:9200/time   --output=http://10.96.83.170:9200/time --type=data 

```

### 4、Other 数据如何导出到本地

```
./elasticdump --ignore-errors=true  --scrollTime=120m  --bulk=true --input=http://10.122.12.234:9200/time   --output=/usr/local/esdump/node-10.122.12.234/data/time.json --type=data  
```







