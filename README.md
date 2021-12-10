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
