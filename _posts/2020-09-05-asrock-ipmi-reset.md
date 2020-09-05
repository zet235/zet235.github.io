---
layout: post
title:  "ASRock IPMI reset"
tags: [env]
---

因為在網路上買了一片 ASRock 的二手 server 主機板，想用 IPMI 的功能，不過密碼已經被改過了，所以上網找一下有沒有可以 reset 的方法

首先可以用個隨便 windows 開機，下載 supermicro 的工具 IPMICFG

<https://www.supermicro.com/SwDownload/SwSelect_Free.aspx?cat=IPMI>

```
ipmicfg -user list

Maximum number of Users          : 10
Count of currently enabled Users : 1
User ID | User Name        | Privilege Level | Enable
------- | ---------        | --------------- | ------
      2 | admin            | Administrator   | Yes

ipmicfg -user setpwd 2 admin
```

或是回到原廠設定

```
ipmicfg -fd
```

[ref]

<https://blog.kingj.net/2014/03/15/how-to/resetting-the-ipmi-password-on-the-e3c224d2i/>
<https://support.siliconmechanics.com/portal/en/kb/articles/resetting-the-bmc>