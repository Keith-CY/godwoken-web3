# Godwoken Web3 API

A Web3 RPC compatible layer build upon Godwoken/Polyjuice.

## Development

### Config database

```
$ cat > ./packages/api-server/.env <<EOF
DATABASE_URL=postgres://username:password@localhost:5432/your_db
GODWOKEN_JSON_RPC=<godwoken rpc>
ETH_ACCOUNT_LOCK_HASH=<eth account lock script hash>
ROLLUP_TYPE_HASH=<godwoken rollup type hash>
EOF
$ yarn
// Only for test purpose
$ yarn workspace @godwoken-web3/api-server reset_database
```

### Start API server

```
yarn workspace @godwoken-web3/godwoken tsc
yarn workspace @godwoken-web3/api-server start
```

## Web3 RPC
### web3_clientVersion

```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"web3_clientVersion","params": [],"id":1}'

// Response
{"jsonrpc":"2.0","id":1,"result":"Godwoken/v1.0.0/darwin/node14.13.1"}
```

### net_version

```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"net_version","params": [],"id":1}'

// Response
{"jsonrpc":"2.0","id":1,"result":"1"}
```

### net_peerCount
```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"net_peerCount","params": [],"id":1}'

// Response
{"jsonrpc":"2.0","id":1,"result":"0x0"}
```
### net_listening
```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"net_listening","params": [],"id":1}'

// Response
{"jsonrpc":"2.0","id":1,"result":true}
```

### eth_protocolVersion
```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_protocolVersion","params": [],"id":1}'

// Response
{"jsonrpc":"2.0","id":1,"result":65}
```

### eth_blockNumber
```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params": [],"id":1}'

// Response
{"jsonrpc":"2.0","id":1,"result":"0x18d}
```

### eth_getBlockByHash

```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_getBlockByHash","params": ["0xb22bb8fd026613ea7674b181261248d38d190419a7870986b6528d4a6622ba0a",false],"id":1}'

// Response
{"jsonrpc":"2.0","id":1,"result":{"number":"0xde","hash":"0xb22bb8fd026613ea7674b181261248d38d190419a7870986b6528d4a6622ba0a","parentHash":"0x03deb171c1d9e703645f3e20e36137f7d918b5b5932f81b5948bdb9092a8e2a4","gasLimit":"0x0","gasLrice":"0x0","miner":"0x0000000000000000000000000000000000000000","size":"0x164","logsBloom":"0x","transactions":["0xbb9d52bb10e36205cb4e7af8c4ac573f609a0f209d095e53f0f66c81b497169b"],"timestamp":0,"mixHash":"0x0000000000000000000000000000000000000000000000000000000000000000","nonce":"0x0000000000000000","stateRoot":"0x0000000000000000000000000000000000000000000000000000000000000000","sha3Uncles":"0x0000000000000000000000000000000000000000000000000000000000000000","receiptsRoot":"0x0000000000000000000000000000000000000000000000000000000000000000","transactionsRoot":"0x0000000000000000000000000000000000000000000000000000000000000000","uncles":[],"totalDifficulty":"0x0","extraData":"0x"}}
```

### eth_getBlockByNumber


```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params": ["0xde",false],"id":1}'

// Response
{"jsonrpc":"2.0","id":1,"result":{"number":"0xde","hash":"0xb22bb8fd026613ea7674b181261248d38d190419a7870986b6528d4a6622ba0a","parentHash":"0x03deb171c1d9e703645f3e20e36137f7d918b5b5932f81b5948bdb9092a8e2a4","gasLimit":"0x0","gasLrice":"0x0","miner":"0x0000000000000000000000000000000000000000","size":"0x164","logsBloom":"0x","transactions":["0xbb9d52bb10e36205cb4e7af8c4ac573f609a0f209d095e53f0f66c81b497169b"],"timestamp":0,"mixHash":"0x0000000000000000000000000000000000000000000000000000000000000000","nonce":"0x0000000000000000","stateRoot":"0x0000000000000000000000000000000000000000000000000000000000000000","sha3Uncles":"0x0000000000000000000000000000000000000000000000000000000000000000","receiptsRoot":"0x0000000000000000000000000000000000000000000000000000000000000000","transactionsRoot":"0x0000000000000000000000000000000000000000000000000000000000000000","uncles":[],"totalDifficulty":"0x0","extraData":"0x"}}
```

### eth_getTransactionByHash

```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc": "2.0", "method":"eth_getTransactionByHash", "params": ["0xbb9d52bb10e36205cb4e7af8c4ac573f609a0f209d095e53f0f66c81b497169b"], "id": 1}'

// Response
{"jsonrpc":"2.0","id":1,"result":{"hash":"0xbb9d52bb10e36205cb4e7af8c4ac573f609a0f209d095e53f0f66c81b497169b","blockHash":"0xb22bb8fd026613ea7674b181261248d38d190419a7870986b6528d4a6622ba0a","blockNumber":"0xde","transactionIndex":"0x0","from":"0x3db4a5310fe102430eb457c257e695795985fd73","to":"0x46beac96b726a51c5703f99ec787ce12793dae11","gas":"0x0","gasPrice":"0x1","input":null,"nonce":"0x1","value":"0xa","v":"0xc4cf76851498d8cb6671c366f2d58e9aa70cf55b998ec4335f1e23dfaeab34","r":"0x3539d9d6018d74b1b9357bab7e16e46f099ba46346ad230854577196f362f3","s":"0x01"}}
```

### eth_getTransactionReceipt
```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc": "2.0", "method":"eth_getTransactionReceipt", "params": ["0xbb9d52bb10e36205cb4e7af8c4ac573f609a0f209d095e53f0f66c81b497169b"], "id": 1}'

// Response
{"jsonrpc":"2.0","id":1,"result":{"transactionHash":"0xbb9d52bb10e36205cb4e7af8c4ac573f609a0f209d095e53f0f66c81b497169b","blockHash":"0xb22bb8fd026613ea7674b181261248d38d190419a7870986b6528d4a6622ba0a","blockNumber":"0xde","transactionIndex":"0x0","gasUsed":"0x0","cumulativeGasUsed":"0x0","logsBloom":"0x","logs":[],"contractAddress":null,"status":"0x1"}}
```

### eth_getTransactionCount

```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc": "2.0", "method":"eth_getTransactionCount", "params": ["0x3db4a5310fe102430eb457c257e695795985fd73"], "id": 1}'

// Response
{"jsonrpc":"2.0","id":1,"result":"0x2"}

```
### eth_gasPrice
```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_gasPrice","params": [],"id":1}'

// Response
{"jsonrpc":"2.0","id":1,"result":"0x1"}
```

### eth_getBalance

```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc": "2.0", "method":"eth_getBalance", "params": ["0x3db4a5310fe102430eb457c257e695795985fd73"], "id": 1}'

// Response
{"jsonrpc":"2.0","id":1,"result":"0x746a5287f6"}

```

### eth_getCode

```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc": "2.0", "method":"eth_getCode", "params": ["0x0500000000000000000000000000000000000000"], "id": 1}'

// Response
{"jsonrpc":"2.0","id":1,"result":"0x60806040526004361060295760003560e01c806360fe47b114602f5780636d4ce63c14605b576029565b60006000fd5b60596004803603602081101560445760006000fd5b81019080803590602001909291905050506084565b005b34801560675760006000fd5b50606e6094565b6040518082815260200191505060405180910390f35b8060006000508190909055505b50565b6000600060005054905060a2565b9056fea2646970667358221220044daf4e34adffc61c3bb9e8f40061731972d32db5b8c2bc975123da9e988c3e64736f6c63430006060033"}

```

### eth_getStorageAt

```
// Request
curl http://localhost:3000 -X POST -H "Content-Type: application/json" -d '{"jsonrpc": "2.0", "method":"eth_getStorageAt", "params": ["0x0c00000000000000000000000000000000000000","0x0"], "id": 1}'

// Response
{"jsonrpc":"2.0","id":1,"result":"0x0000000000000000000000000000000000000000000000000000000000000d10"}
```

### eth_call

### eth_estimateGas