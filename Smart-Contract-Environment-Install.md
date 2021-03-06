## Pre-Install ##
```
sudo apt-get update
sudo apt-get install openssl libtool autoconf automake uuid-dev build-essential gcc g++ python-software-properties unzip make git libcap2-bin -y
```

## Install Parity ##
```
bash <(curl https://get.parity.io -kL)
```

## Docs ##
https://github.com/paritytech/parity/wiki/Setup  
https://github.com/paritytech/parity/wiki/Configuring-Parity  

## mainnet.toml ##
```
[parity]
mode = "active"
base_path = "/home/ubuntu/baliv-parity/"

[footprint]
tracing = "off"
pruning = "fast"
db_compaction = "ssd"
cache_size = 4096

[network]
port = 30303
min_peers = 50
max_peers = 100

[rpc]
interface = "0.0.0.0"
port = 8545
apis = ["web3", "eth", "net", "personal", "parity", "parity_set", "traces", "rpc", "parity_accounts"]
```

## config.toml ##
chain = "/home/ubuntu/Baliv-Parity/genesis.json"
path = /home/ubuntu/snap/parity/6787/.local/share/io.parity.ethereum/config.toml
```
[parity]
chain = "dev"
base_path = "/home/ubuntu/Baliv-Parity"

[network]
port = 30300

[mining]
author = "0x582f459aa7d9c16df55e42bcca3efefd968b42d3"
engine_signer = "0x582f459aa7d9c16df55e42bcca3efefd968b42d3"

[account]
unlock = ["0x582f459aa7d9c16df55e42bcca3efefd968b42d3"]
password = ["/PATH/TO/PASSWORD/FILE"]
keys_iterations = 10240

[rpc]
interface = "0.0.0.0"
port = 8545
apis = ["web3", "eth", "net", "personal", "parity", "parity_set", "traces", "rpc", "parity_accounts"]

[websockets]
disable = false
port = 8546
interface = "0.0.0.0"
origins = ["none"]
apis = ["web3", "eth", "net", "parity", "traces", "rpc", "secretstore"]
hosts = ["none"]

[ui]
force = false
disable = false
port = 8180
interface = "0.0.0.0"
path = "/home/ubuntu/Baliv-Parity/signer"

[dapps]
jsonrpc-port = 8080
```

## Genesis ##
```json
{
    "name": "Baliv-Chain",
    "engine": {
        "authorityRound": {
            "params": {
                "stepDuration": "1",
                "validators" : {
                    "list": []
                }
            }
        }
    },
    "params": {
        "gasLimitBoundDivisor": "0x400",
        "maximumExtraDataSize": "0x20",
        "minGasLimit": "0x5208",
        "networkID" : "0x1"
    },
    "genesis": {
        "seal": {
            "authorityRound": {
                "step": "0x0",
                "signature": "0x0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"
            }
        },
        "difficulty": "0x20000",
        "gasLimit": "0x5B8D80"
    },
    "accounts": {
        
    }
}
```

### create account (key) ###
parity account new --chain /PATH/TO/GENESIS --keys-path /PATH/TO/KEY/FOLDERS

### 啟動 Parity ###
parity --config /PATH/TO/CONFIG.toml

### 啟動 Parity on kovan ###
parity --chain kovan --port 30303 --jsonrpc-port 8545 --ui-port 8180 --dapps-port 8080 --jsonrpc-apis web3,eth,net,personal,parity,parity_set,traces,rpc,parity_accounts

### SSH Tunnel ###
https://github.com/paritytech/parity/wiki/Wallet-Remote-Access
```
ssh -i key.pem -L 8545:127.0.0.1:8545 -L 8546:127.0.0.1:8546 -L 8180:127.0.0.1:8180 <user>@<host> -vv
```

### 產生可連上parity的token ###
parity signer new-token --ui-port 8180

### 連接上述產生的token URL ###
curl 127.0.0.1:8180/#/auth?token=HFi7-7HJf-Shcd-mZie
