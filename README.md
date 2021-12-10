# odin-protocol-tools

Some tools and scripts for the [Odin Protocol](https://odinprotocol.io/)

## One-liner script `run_odin_node.sh`

Script for quick node installation 

1) creates an odin user
2) downloads `odind`, `yoda` binary and installs them in `/usr/local/bin/`
3) downloads `libgo_owasm.so` and installs it in /usr/lib/
4) if the `/home/odin/.odin` directory doesn't already exist, scrip will 
  * initialize the node 
  * loads official genesis from github, checks it for sha256 
  * unsafe-reset-all
5) Set seeds and persistent_peers in config.toml from github
6) Set minimum gas prices to 0.0125loki
7) Install and run the service

You can run the script as follows and it will install v0.1.0 odind by default
```bash
curl -sL https://mercury-nodes.net/run_odin_node.sh | sudo bash -s -- YOUR_NODE_NAME
```

P.S. If you want to experiment with v0.2.0 you can run the script like this
```bash
curl -sL https://mercury-nodes.net/run_odin_node.sh | sudo VERSION=v0.2.0 bash -s -- YOUR_NODE_NAME 
```

Official guide to run a validator in the Odin Mainnet
https://github.com/ODIN-PROTOCOL/networks/tree/master/mainnets/odin-mainnet-freya

## Seeds vs persisten_peers

We created seed node, you can use it in addition with the main one. 
4529fc24a87ff5ab105970f425ced7a6c79f0b8f@odin-seed-01.mercury-nodes.net:29536

Moreover, using `seeds` is preferable to `persistent_peers`, i.e. you can delete all `persistent_peers` in your `config.toml` and leave only `seeds`

```bash
SEEDS="4529fc24a87ff5ab105970f425ced7a6c79f0b8f@odin-seed-01.mercury-nodes.net:29536,f283528c5781680267509208f9ae993b28ee7512@odin-seed.blockpane.com:26656"

sed -i.bak -e "s/^seeds =.*/seeds = \"$SEEDS\"/" -e 's/^persistent_peers *=.*/persistent_peers = ""/' ~/.odin/config/config.toml

service odind restart
```

Seed nodes are designed precisely to collect information about the active nodes involved in the p2p exchange, which allows other nodes to ask them for actual addresses and form the most appropriate connections, instead of trying to constantly communicate with persistent_peers, even when they are not working or are overloaded and do not allow new connections. 
