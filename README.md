# Kœri-Coin

The (yet) unofficial cryptocurrency of the glorious
superior elite university Karlruhe Institute of Karlsruhe.

![Koericoin logo](https://github.com/koericoin/koericoin/raw/master/koeri_alpha_1000px.png)

[Koericoin on Reddit](https://www.reddit.com/r/koericoin/)  
[Koericoin on Discord](https://discord.gg/aZuH5WeDcg)


## List of current bootstrap nodes

- `enode://58a467f03de6da5877a8e8afaa3cbb3d0927613262ec7fee657ce2a0dd891fc56301f86edf4ebcff479ee9e04efa439f7bc7759ac5b647cd236713cc96785fcc@5.45.106.216:30303`
- `enode://8d41b7303764e4b64baec3b1df7cc3c793264e6d7735a9b7dcc4d675957e7c19bd258610dcd08a056d1297fb636988a5770c6fddc0f20a48cf5dfb6c138b477c@159.69.245.187:30303`
- `enode://44c33cba8acb932bc88e441caaace6cc8696525ebce7544eb59e22768152a4cb0da8ee226b1134610554a2db0d363c02abafd355fbf7db00630a2f5df7699eba@5.9.120.174:30305`

## How to run a Koericoin node
Koericoin currently is a seperated Ethereum chain, to profit
from maximum functionality an stability.


###  ___First___
Download the ethereum client [geth](https://geth.ethereum.org/downloads/).

###  ___Second___
Create the genesis file `genesis.json`.
```json
{
  "config": {
    "chainId": 1415926,
    "homesteadBlock": 0,
    "eip150Block": 0,
    "eip155Block": 0,
    "eip158Block": 0,
    "byzantiumBlock": 0,
    "constantinopleBlock": 0,
    "petersburgBlock": 0,
    "ethash": {}
  },
  "difficulty": "1",
  "gasLimit": "8000000",
  "alloc": {
    "7df9a875a174b3bc565e6424a0050ebc1b2d1d82": { "balance": "0" },
    "f41c74c9ae680c1aa78f42e5647a62f353b7bdde": { "balance": "0" }
  }
}
```

### ___Third___
Initialize the genesis block and generate a blockchain directory.  
`geth init --datadir koerichain genesis.json`

### ___Forth___
Start the node.  
Replace the invalid bootstrap nodes with vali ones from [list of current bootstrap nodes](#list-of-current-bootstrap-nodes).
```bash
geth --datadir koerichain \
    --networkid 1415926 \
    --port 30303 \
    --bootnodes "enode://123@ip:port,enode://123@ip:port"
```

## Become a bootstrap node
A bootstrap node is an entry point for new nodes. There they can connect
to the blockchain without searching.
Therefore bootstrap nodes should stay up for a long term.

This also means you have to update some configuation, if we decide to do a
hard fork.

If you are dedicated enough to run one, follow the instructions below and ask
to be added to the list of 
[list of current bootstrap nodes](#list-of-current-bootstrap-nodes).

### ___First___
Follow
[how to run a Koericoin node](#how-to-run-a-Koericoin-node).

### ___Second___
Configure your
[Brandschutzmauer](https://en.wikipedia.org/wiki/Firewall_(computing))
to allow incoming UDP and TCP connections
of your configured port (default `30303`)
to reach your server.

### ___Third___
Run your node explicit with your public ip address:
```
geth --datadir koerichain \
    --networkid 1415926 \
    --nat extip:123.123.123.123
    --port 30303 \
    --bootnodes "enode://123@ip:port,enode://123@ip:port"
```

### ___Forth___
Extract your enode address to be published.  
In another terminal run  
`./geth attach koerichain/geth.ipc --exec admin.nodeInfo.enode`

This is the address we can add to the list of bootstrap nodes.

## How to mine (CPU)
### ___First___
[Get a geth wallet](#get-a-wallet).  
Copy your public key.

### ___Second___
Follow
[how to run a Koericoin node](#how-to-run-a-Koericoin-node).

###  ___Third___
Activate mining when starting your node.
Replace the etherbase with your public key.  
Set the size of your [Fadenschwimmbecken](https://en.wikipedia.org/wiki/Thread_pool) by replacing
`--minerthreads=1`.
```bash
geth --datadir koerichain \
    --networkid 1415926 \
    --port 30303 \
    --bootnodes "enode://123@ip:port,enode://123@ip:port" \
    --mine --minerthreads=1 \
    --etherbase=0x0000000000000000000000000000000000000000
```

## How to mine (GPU)
Start geth as a kind of local mining pool and connect
to it with ethminer.


### ___First___
Start geth with rpc activated. Replace the etherbase with your wallet and
the bootnodes with the bootnodes from
[list of current bootstrap nodes](#list-of-current-bootstrap-nodes).
```bash
geth --datadir koerichain \
    --networkid 1415926 \
    --port 30303 \
    --bootnodes "enode://123@ip:port,enode://123@ip:port" \
    --mine \
    --rpc \
    --etherbase=0x0000000000000000000000000000000000000000
```

### ___Second___
Get ethminer from [GitHub](https://github.com/ethereum-mining/ethminer).

### ___Third___
Start ethminer.
```bash
# Cuda:
ethminer -U -P http://127.0.0.1:8545/
# AMD:
ethminer -G -P http://127.0.0.1:8545/
```


## Get a wallet
TODO  
[Wallets with geth](https://geth.ethereum.org/docs/interface/managing-your-accounts)
