# ethereum bash

```bash
brew install geth
geth --datadir=./data --ethash.dagdir=./ethash init genesis.json
geth --datadir=./data account new --password=<(echo password) 
// get the ether base from last command
geth --datadir "./data" --ethash.dagdir=./ethash --nodiscover --etherbase="0x68deb77c5c8c5b72f1d82a1921d6369195f61dd1" --mine --minerthreads=4 --verbosity=4
```