# ethereum bash

## standalone mode
```bash
brew install geth
geth --datadir=./data --ethash.dagdir=./ethash init genesis.json
geth --datadir=./data account new --password=<(echo password) 
// get the ether base from last command
geth --datadir "./data" --ethash.dagdir=./ethash --nodiscover --etherbase="0x68deb77c5c8c5b72f1d82a1921d6369195f61dd1" --mine --minerthreads=4 --verbosity=4
```


## cluster mode
```bash
bootnode -genkey ./bootnode/boot.key
bootnode --nat=none --nodekey ./bootnode/boot.key --verbosity=4 --addr="0.0.0.0:30301"
//copy the output and replace "[::]" with 127.0.0.1 of last output
// the --bootnodes value is from the last output
geth --datadir=./data account new --password=<(echo password)
geth --networkid=331788 --datadir=./data --ethash.dagdir=./ethash_node \
    --bootnodes="enode://4a8ec0f05a48bc4c014a0426c868d76617d445e6ade36d74d1ba44d88db2d939328b08012a6ec5e046c29ba08ac9050a4cbd3d79ba2a4cd261b96c18c3556ee5@127.0.0.1:30301"
   
geth --datadir=./miner account new --password=<(echo password)  
geth --networkid=331788 --datadir=./miner --ethash.dagdir=./ethash_miner \
    --bootnodes="enode://4a8ec0f05a48bc4c014a0426c868d76617d445e6ade36d74d1ba44d88db2d939328b08012a6ec5e046c29ba08ac9050a4cbd3d79ba2a4cd261b96c18c3556ee5@127.0.0.1:30301" \
    --etherbase="0xf04c32e10f4e6572aeea15a08b9686e29ea83737" --mine --minerthreads=4 --verbosity=4 --port=30304 console
    
    
# validation for the mine result
geth --datadir=./data attach
// then execute the next
eth.getBalance("0xf04c32e10f4e6572aeea15a08b9686e29ea83737") 
```