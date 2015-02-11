---
title: Saltstack Config
layout: post
---

### Saltstack 基本架構

### Saltstack 安裝 (以 Ubuntu 14.04 為例)

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

在 Ubuntu 中安裝 Saltstack 很簡單, 只要透過 apt-get 安裝相關套件即可, 安裝完成之後, 系統中便已經有了 Salt Master 及 Minion, 接著可開始進行設定的步驟!

```
sudo apt-get install salt-master
sudo apt-get install salt-minion
```

### Saltstack 設定

#### 修改 Minion 設定檔及傳送公開金鑰

Minion 啟動時會嘗試去連線 Master, 若沒有特別設定 Master 的 hostname, 則預設為 salt! Minion 第一次與 Master 連線時, 會將自己的 id 及公開金鑰傳遞給 Master, 並且 請求 Master 接受, Minion 會在 Master 接受公開金鑰之後才能接受 Master 所指派的指令!
所以在首次啟動 Minion 之前, 需修改 Minion 的設定檔 (/etc/salt/minion), 加入以下兩個設定:

```
master: master-hostname
id: minion-id
```

#### Master 接受 Minion 之公開金鑰

Master 可使用 salt-key 指令來顯示及接受 Minions 所送出的公開金鑰!

```
salt-key -L (在 master 上顯示所有以接受及未接受之金鑰)
```

```
salt-key -A (Master 用以接受所有金鑰)
```

```
salt-key -f minion-id (在 master 上顯示 minion-id 所傳送的金鑰內容)
```

```
salt-call key.finger --local (在 minion 上顯示本地端的金鑰內容)
```

```
salt-key -a minion-id (在 master 上接受 minion-id 的金鑰)
```

#### 連線及指令測試

第一個測試指令: 回應 Master 的呼叫

```
salt '*' test.ping
```

```*``` 為執行指令的目的端, ```test``` 為執行模組 (Execution module), ```ping``` 為被執行的指令或函式!

第二個測試指令: 顯示磁碟使用狀況

```
salt '*' disk.usage
```


