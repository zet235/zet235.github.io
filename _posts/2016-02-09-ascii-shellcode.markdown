---
layout: post
title:  "ascii shellcode"
tags: [shellcode]
---

可以使用`alpha3`這套工具，他會產生出具有encoder的ascii shellcode ， 利用本身的encoder去解碼，產生出來的shellcode很短，不過這類的shellcode需要一個`reg`去指向shellcode的起頭

其他別種的有些是利用偏移去xor，最後`jmp esp`去執行

紀錄一下一題題目的解法：
利用stack上的位置跟`ROP`的`ret`跳到那個位置上，再利用stack上的值去跟eax去做xor，利用的是像`xor al,[esp+0x34]`這類的op code，偏移的部分利用`push eax` 來填充，最後剛好使eax 指向我們shellcode的位置

可以參考下方的參考資料

#### References:

```
http://inaz2.hatenablog.com/entry/2014/07/11/004655
http://inaz2.hatenablog.com/entry/2014/07/12/000007
http://inaz2.hatenablog.com/entry/2014/07/13/025626
https://code.google.com/archive/p/alpha3/
https://nets.ec/Ascii_shellcode
```