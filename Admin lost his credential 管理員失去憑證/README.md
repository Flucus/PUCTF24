## Admin lost his credential 管理員失去憑證

Assume I have created an account username=adminn, password=adminn 
The cookies (identity) would be WmOm6E638GaMmei2Qz9BLE50rvNO69ti3Yvp
The encryption and decryption is using Binary XOR with the server random key. Then I used the plain_text and cipher_text to find out the server random key.

```py
# from gevent import pywsgi
import base64
def find_key(plain_text, cipher_text):
    plain_bytes = plain_text.encode()
    cipher_bytes = base64.b64decode(cipher_text)
    key = [p ^ c for p, c in zip(plain_bytes, cipher_bytes)]
    return bytes(key)

# 使用範例：
plain_text = 'username=adminn&admin=False'  # 替換為您的明文
cipher_text = 'WmOm6E638GaMmei2Qz9BLE50rvNO69ti3Yvp'  # 替換為您的Base64編碼的密文
key = find_key(plain_text, cipher_text)
print('Key:', key)

def decrypt(cipher):
    buf = bytes.fromhex(base64.b64decode(cipher).hex())
    i = 0
    output = []
    for b in buf:
        output.append( b ^ key[i % len(key)] )
        i = i + 1
    output = bytes(output).decode()
    return output

print(decrypt('WmOm6E638GaMmei2Qz9BLE50rvNO69ti3Yvp'))

def encrypt(content):
    buf = content.encode()
    i = 0
    output = []
    for b in buf:
        output.append( b ^ key[i % len(key)] )
        i = i + 1
    output = base64.b64encode(bytes(output)).decode()
    return output

print(encrypt('username=adminn&admin=True'))
```

Welcome, adminn! Here is your flag: PUCTF24{y0u_kn0w_h0w_t0_b5c0m5_adm1n15tr4t0r_3af9b6a0718c4e239d5c6fe802b9e517}
(This is a secret for admin only)

I replaced the cookies(identity) with the encrypted text by using the above program.