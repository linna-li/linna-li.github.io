---
title: "安装prometheus"
author: "linna.li"
tags: ["raspberry"]
categories: ["note"]
date: 2020-01-30
---
> 成果：安装prometheus的node-exporter来导出server的metrics。prometheus是用来收集metrics的，grafana通过pull的方式去拿数据，然后进行显示。除了prometheus之外也有其他的datasource，比如influxdb，是通过push的方式来向grafana发送数据。
参考文档：https://computingforgeeks.com/how-to-monitor-linux-server-performance-with-prometheus-and-grafana-in-5-minutes/

这个文档也是没有用apt指令，是通过APT仓库进行安装。但是我搞错了版本，应该用 *ARM64*的版本，但是我用的是amd64。amd64是x86-64, 后来只能清理了所有的node-exporter，直接用apt重新安装的。（用 lsb_release -a可以看到ubuntu版本）

```
sudo apt install prometheus-node-exporter
sudo systemctl daemon-reload
sudo systemctl start prometheus-node-exporter
sudo systemctl enable prometheus-node-exporter
sudo systemctl status prometheus-node-exporter
```
成功之后发现从server的local可以看到metrics，但是用mac上用 curl -GET http://localhost:9100/metrics 没有办法。
用指令来检查端口的开放情况
sudo ufw status verbose
发现9100端口没有开放
用指令开放：sudo ufw allow 9100/tcp
![](/images/port.png)
因为不熟悉ubuntu server的文件结构，所以出错了也不知道应该改哪个文件，只能参考这个文档尽量做到清除干净：
http://www.linfo.org/var.html
https://superuser.com/questions/513159/how-to-remove-systemd-services

安装 sudo apt  install tree 可以来看到文件结构。command: tree workspace/
node_exporter.service文件可以自己customized。如果用apt下载，这个文件会被叫做prometheus-node-exporter.service
```
$ cat data/node_exporter.service
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```

### 关于为什么不用apt