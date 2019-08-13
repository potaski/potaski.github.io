---
layout: post
title:  "IT运维监控平台规划"
categories: 运维
tags: 运维 监控 zabbix grafana
author: ZhangWei
---

* content
{:toc}

> 最近设计了公司监控系统，已向高层汇报；会上沟通还不错，领导也非常认可
>
> 这边现在来总结分享设计思路及监控方案

## 背景条件

首先是业务系统多、团队多，而且还有不少流动的厂商及外包人员

所以这里面就有一个规划的问题，包括监控点、日志格式是否统一

目前上述这些都是单打独斗，无整体规划的

其次是目前对监控系统的需求性不高，底层有公有云提供的稳定服务和简单监控

业务层面有业务人员报障，也有业务运维针对关键业务编写了监控脚本

其余的非关键业务，则对服务的可用性没有那么高要求

最后是已经有部分监控系统在做测试及试用：Grafana/Prometheus/ELK

基于以上背景，和公司提出的一些需求（特别是网络拓扑图），在研究了主流的开源产品后

Zabbix/Prometheus/OpenFalcon

数据处理还是使用zabbix吧，开箱即用，web管理界面做的好

## 架构概要

![m9Ktyt.png](https://s2.ax1x.com/2019/08/13/m9Ktyt.png)

由grafana负责数据可视化，zabbix系统负责数据的采集和分析处理

当前zabbix版本为4.2，感觉更加开放了，支持数据推送、支持Prometheus

但是仍然有不少缺点，api有点啰嗦（个人觉得），web操作繁琐

所以我大量使用了zabbix的discovery功能生成监控

## 管理平台

![m9GgC8.png](https://s2.ax1x.com/2019/08/13/m9GgC8.png)

为了方便（偷懒）监控配置，单独写了一个统一管理平台，可以说是一种CMDB

但是不想把话说那么满，仅是用来维护监控对象的一套系统

同样是 django + jq 一把梭

把django用成不是django的样子，改天可以再单独写写这个内容

![m9GL2F.png](https://s2.ax1x.com/2019/08/13/m9GL2F.png)

通过录入一些业务主机的基本信息，再辅以zabbix的自动发现，可以快速生成监控配置

部分 discovery 脚本：

``` shell
discovery_app_monitor_script.py
discovery_business_child_node.py
discovery_business.py
discovery_db_backup_ip.py
discovery_host_monitor.py
discovery_jvm_app.py
discovery_wan_ip.py
```

我觉得挺方便的，各位业务运维同仁可以自己维护信息，我就可以休息了

同时也可以录入系统间调用关系，达到监控业务A -> B端调用是否正常等等

利用这些信息用来绘制一个系统的拓扑图，但目前仅监控了由A -> B端端口

更详细的业务层面探测，还未开始进行

![m9JosH.png](https://s2.ax1x.com/2019/08/13/m9JosH.png)

根据信息绘制的关系图

[![m9JTLd.md.png](https://s2.ax1x.com/2019/08/13/m9JTLd.md.png)](https://imgchr.com/i/m9JTLd)

本来想根据关系直接生成zabbix上的系统拓扑图，但是内容太多，一时掌握不了

目前还是手动配置中

## 后续展望

对于整个框架我觉得是没有什么问题了，当前的能力也就做到这样了

继续在细节上完善，引入日志分析，告警聚合等

外部界面再加个壳就可以做成产品出售了，呵呵。
