## json-rpc ##
### eth_call ###
呼叫 smart contract function

- 取得 smart contract 位址
- 取得函式名稱與參數格式
- 將前述資料進行 keccak-256 處理後取前十位字串(含 0x)並補上 24 個 0
- 將前述資料加上參數資料（長度須參考[資料格式](http://solidity.readthedocs.io/en/develop/types.html)定義）

### eth_sendRawTransaction ###
執行交易或 smart contract

- 交易資訊需使用 [RLP](https://github.com/ethereum/wiki/wiki/RLP) 轉換
- 使用 [secp256k1](https://en.bitcoin.it/wiki/Secp256k1) 演算法簽屬
```
{
   nonce: '00',
   gasPrice: '09184e72a000',
   gasLimit: '2710',
   to: '0000000000000000000000000000000000000000',
   value: '00',
   data: '7f7465737432000000000000000000000000000000000000000000000000000000600057',
   v: '1c',
   r: '5e1d3a76fbf824220eafc8c79ad578ad2b67d01b0c2425eb1f1347e8f50882ab',
   s: '5bd428537f05f9830e93792f90ea6a3e2d1ee84952dd96edbae9f658f831ab13'
}
```
