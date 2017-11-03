## json-rpc ##
### eth_call ###
呼叫 smart contract function

- 取得 smart contract 位址
- 取得函式名稱與參數格式
- 將前述資料進行 sha3 處理後取前十位字串並補上 24 個 0
- 將前述資料加上參數資料（長度須參考[資料格式](http://solidity.readthedocs.io/en/develop/types.html)定義）
