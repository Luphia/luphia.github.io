## Install Parity ##
```
bash <(curl https://get.parity.io -kL)
```

## Docs ##
https://github.com/paritytech/parity/wiki/Setup
https://github.com/paritytech/parity/wiki/Configuring-Parity

### 啟動parity on kovan ###
parity --chain kovan --port 30303 --jsonrpc-port 8545 --ui-port 8180 --dapps-port 8080 --jsonrpc-apis web3,eth,net,personal,parity,parity_set,traces,rpc,parity_accounts

### 產生可連上parity的token ###
parity signer new-token --ui-port 8180

### 連接上述產生的token URL,也可用curl測試,注意只能在本機,且要用127.0.0.1 ###
curl 127.0.0.1:8180/#/auth?token=HFi7-7HJf-Shcd-mZie
