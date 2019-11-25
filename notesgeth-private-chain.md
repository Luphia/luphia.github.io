## Install Golang
```shell
sudo add-apt-repository ppa:longsleep/golang-backports
sudo apt-get update
sudo apt-get install golang-go
```

## Install Library
```shell
sudo apt-get update
sudo apt-get install openssl libtool autoconf automake uuid-dev build-essential gcc g++ python-software-properties unzip make git libcap2-bin golang-go -y
git clone https://github.com/ethereum/go-ethereum
cd go-ethereum
make all
sudo ln -s /.../build/bin/geth /usr/local/bin/
sudo ln -s /.../build/bin/puppeth /usr/local/bin/
```

## Make New Account
```shell
geth --datadir ./data/ account new
```

## Create Genesis
```shell
vi genesis.json
```
```json
{
    "config": {
        "chainId": 1,
        "homesteadBlock": 0,
        "eip150Block": 0,
        "eip155Block": 0,
        "eip158Block": 0
    },
    "difficulty": "200000000",
    "gasLimit": "8000000",
    "alloc": {
        "a1ad6cD15F4582122261E7C05fbAfA36FDC8f3D8": { "balance": "10000000" },
        "0948644EAcB2dF563C207ac2AFB9f55D3bE42637": { "balance": "10000000" },
        "0155AAFDb6417A0c6B86Ed8938679Ea0B8D9fCE8": { "balance": "10000000" }
    }
}
```

## Start Service
```shell
vi geth.sh
```
```shell
geth --datadir ./data --mine --minerthreads=1 --etherbase=0155AAFDb6417A0c6B86Ed8938679Ea0B8D9fCE8 \
--rpc --rpcaddr 0.0.0.0 --rpcport 8545 --rpcapi db,admin,debug,eth,miner,net,personal,rpc,txpool,web3 --rpccorsdomain "*"\
--ws --wsaddr 0.0.0.0 --wsport 8546 --wsapi db,admin,debug,eth,miner,net,personal,rpc,txpool,web3 --wsorigins "*"
```
```shell
vi keep.sh
```
```shell
n=0
until [ $n -ge 5 ]
do
   sh /home/ubuntu/geth.sh && break  # substitute your command here
   n=$[$n+1]
   sleep 15
done
```
