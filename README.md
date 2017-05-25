# Factory

This repository is workshop for sonm smart-contracts organisation.


See presale and token contracts here:
(https://github.com/sonm-io/token)

Contracts schematic could be found here :
(https://github.com/sonm-io/Contracts-scheme)



## Golang artefacts

 Golang artefacts of solidity contracts is used for bindings contract to native golang applications.

 You can find golang artefacts in ```contracts``` directory

 To generate artefact from source you should install ```abigen``` first.

 Abigen is a tool from ```go-ethereum``` package.

### Abigen install

 First you need to install godep tool by

 ```go get github.com/tools/godep```

  Then you should install abigen itself

  ```
  cd $GOPATH/src/github.com/ethereum/go-ethereum
  godep go install ./cmd/abigen
  ```



 If something wrong with abigen dependency (like someone forget to check broken dep from abigen in official go-ethereum)
  you could try just ```go install abigen ``` from  ```./cmd/``` directory.

  You should see your abigen binary in  ```/bin/``` your $GOPATH directory.


### Generating go artefacts

  You should use proper way to generate golang bindings from source ```.sol``` files.

  ```abigen --sol token.sol --pkg main --out token.go ```

  Where the flags are:

    --abi: Mandatory path to the contract ABI to bind to
    --pgk: Mandatory Go package name to place the Go code into
    --type: Optional Go type name to assign to the binding struct
    --out: Optional output path for the generated Go source file (not set = stdout)


  this command will generate go bindings from your token.sol contract and you can further use it in your go application.

  note, that if you will use ```--type``` flags as
  ```abigen --abi token.abi --pkg main --type Token --out token.go```

  it will create new ```Token``` struct for your go project and you can be use this struct without neccesarry to import your generated file into main project.
  This is simplier way to develop, but may be confusing when you would not remember where do you declarated this struct and how to change it.

  note - you **have to ** store zeppelin library in contracts directory because apigen does not recognise ethpm folders as truffle do.

  ### GO generate
  You can generate go binds from sol files by ```go generate``` see more info in ```generator.go``` in contracts directory.

  To generate packages you need to run in console ```go generate``` in contracts directory. Generated files will be saved in ```/go-build/``` directory.

  # Rinkbey Testnet

  To run rinkey testnet through go-ethereum node you should run it as follows:

  ```
  geth --networkid=4 --datadir=$HOME/.rinkeby --cache=512 --ethstats='yournode:Respect my authoritah!@stats.rinkeby.io' --bootnodes=enode://a24ac7c5484ef4ed0c5eb2d36620ba4e4aa13b8c84684e1b4aab0cebea2ae45cb4d375b77eab56516d34bfbd3c1a833fc51296ff084b770b94fb9028c4d25ccf@52.169.42.101:30303 --rpc --password <(echo yourpassword) --unlock 0 --rpccorsdomain localhost

```

  To attach official ethereum foundation wallet
  ```
  ethereumwallet --rpc $HOME/.rinkeby/geth.ipc --node-networkid=4 --node-datadir=$HOME/.rinkeby --node-ethstats='yournode:Respect my authoritah!@stats.rinkeby.io' --node-bootnodes=enode://a24ac7c5484ef4ed0c5eb2d36620ba4e4aa13b8c84684e1b4aab0cebea2ae45cb4d375b77eab56516d34bfbd3c1a833fc51296ff084b770b94fb9028c4d25ccf@52.169.42.101:30303
```

 ## Rinkbey testnet contract addresses:

 Migrations: 0x97b476511a9b2719c1aba209641624998e397392
 SDT: 0x31ac2908b1f981519b7ab992b46eaa41566b3c0a
 Factory: 0x1d978c1a1f7f15b624f13b4f8400ed28ed48c54f
 Whitelist: 0x638724e6dd02b641a186c3dc926fe773a1c1554f
