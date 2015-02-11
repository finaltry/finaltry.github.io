---
title: Saltstack Config
layout: post
---

### Saltstack 簡介

### Saltstack (以 Ubuntu 14.04 為例)

#### 新增 Ubuntu Repository

在 Ubuntu 中要安裝 Saltstack 之前, 需先以如下指令將 Saltstack 的 PPA 加入 source repository:

```
sudo add-apt-repository ppa:saltstack/salt
```

PPA設定完成後, 應該可在 /etc/apt/sources.list.d 中找到 saltstack-salt-trusty.list 檔案! 如果系統中沒有 add-apt-repository, 則表示缺少 python-software-properties, 先執行以下指令安裝:

```
sudo apt-get install python-software-properties
```

#### 安裝 Saltstack Master 及 Minion
