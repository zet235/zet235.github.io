---
layout: post
title:  "Use TTL to unbrick router"
---

之前刷 Router 的時候不小心把它刷爆了，變成磚，可以透過 FT232 工具把 Router 的殼拆掉，對接上面的 RS232，其中 GND, TX, RX 接到電腦可以直接下 command，也可以執行 system shell。

使用 Putty 連接 FT232 的 COM Port，至於Router板子上面的腳位可以透過 DD-WRT 或是 Open-WRT 中的 Wiki，幾乎很多路由器都有可以參考的資料。

例如：[https://wiki.openwrt.org/toh/d-link/dir-300revb](https://wiki.openwrt.org/toh/d-link/dir-300revb)

接上以後會出現以下選單，手速要快一點，選擇 "2" 可以連接到電腦架設的 TFTP Server 抓取韌體並重刷。
```
   Please choose the operation:
   1: Load system code to SDRAM via TFTP.
   2: Load system code then write to Flash via TFTP.
   3: Boot system code via Flash (default).
   4: Entr boot command line interface.
   7: Load Boot Loader code then write to Flash via Serial.
   9: Load Boot Loader code then write to Flash via TFTP.
```

電腦設定固定 ip，然後網路線連到 Router，輸入電腦 ip 與韌體的檔名就好了。