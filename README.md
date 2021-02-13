# Kœri-Coin

The (yet) unofficial cryptocurrency of the glorious
superior elite university Karlruhe Institute of Karlsruhe.

![Koericoin logo](https://github.com/koericoin/koericoin/raw/master/koeri_alpha_1000px.png =20%x)

[Koericoin on Reddit](https://www.reddit.com/r/koericoin/)  
[Koericoin on Discord](https://discord.gg/aZuH5WeDcg)


## List of current bootstrap nodes

- Hosted by Julian6bG: `enode://58a467f03de6da5877a8e8afaa3cbb3d0927613262ec7fee657ce2a0dd891fc56301f86edf4ebcff479ee9e04efa439f7bc7759ac5b647cd236713cc96785fcc@5.45.106.216:30303`



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
`./geth attach data/geth.ipc --exec admin.nodeInfo.enode`

This is the address we can add to the list of bootstrap nodes.

## How to mine (CPU)
### ___First___
[Get a geth wallet](#get-a-wallet).  
Copy your public key.

### ___Second___
Follow
[how to run a Koericoin node](#how-to-run-a-Koericoin-node).

###  ___Thirs___
Activate mining when starting your node.
Replace the etherbase with your public key.
```bash
geth --datadir koerichain \
    --networkid 1415926 \
    --port 30303 \
    --bootnodes "enode://123@ip:port,enode://123@ip:port" \
    --mine --minerthreads=1 \
    --etherbase=0x0000000000000000000000000000000000000000
```

## How to mine (GPU)
TODO

## Get a wallet
TODO  
[Wallets with geth](https://geth.ethereum.org/docs/interface/managing-your-accounts)
