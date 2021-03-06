[![Join the chat at https://gitter.im/fork-ethereum/Lobby](https://badges.gitter.im/fork-ethereum/Lobby.svg)](https://gitter.im/fork-ethereum/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

# Installation

## Docker

[Install Docker](https://www.docker.com/community-edition)

_Dockerfile_

https://hub.docker.com/r/forkblockchain/fork-ethereum/

docker pull forkblockchain/fork-ethereum:latest

or 

_Docker compose_

docker-compose up -d

then

./enter-docker.sh

cd /ethereum

## Vagrant

[Install VirtualBox](https://www.virtualbox.org/wiki/Downloads)

[Install Vagrant](https://www.vagrantup.com/docs/installation/)

vagrant up --provision

cd /home/ethereum/

# Initialization of Chain

_geth Commands_

./init-genesis.sh

./start-geth.sh 

./connect-geth.sh


# Account Setup Commands

_Create New Account_

personal.newAccount();

or (need to specify passpharse as argument in container)

personal.newAccount("YOUR PASSPHRASE");

_Show Balance_

eth.getBalance(eth.accounts[0]);

_Generate DAG and mine coins_

miner.start();

miner.stop();

# Smart Contract Example
_Contract Commands_

loadScript("simple.js")

var parsedSimpleContract = web3.eth.contract(JSON.parse(simpleContract.contracts["simple.sol:Simple"].abi));

personal.unlockAccount(eth.accounts[0], "YOUR PASSPHRASE");

_Log mined contract_
```
var simpleContract = parsedSimpleContract.new({ from: eth.accounts[0], data: "0x" + simpleContract.contracts["simple.sol:Simple"].bin, gas: 4700000},
  function (e, contract) {
    console.log(e, contract);
    if (typeof contract.address !== 'undefined') {
         console.log('Contract mined! address: ' + contract.address + ' transactionHash: ' + contract.transactionHash);
    }
  }
);
```

_Mine contract_
miner.start();

miner.stop();

_Execute locally_

simpleContract.multiply.call(9,2);

_Execute on evm_

simpleContract.multiply.sendTransaction(2,2,{from:eth.accounts[0]})

_Process smart contract transaction_

miner.start();

miner.stop();

_View Logged Events_

var simpleContractEvents = simpleContract.allEvents({fromBlock: 0, toBlock: 'latest'});

```
simpleContractEvents.get(function(error, logs) {
  logs.forEach( function(log,error) {
    console.log(JSON.stringify(log.args));
  })
});
```

# References

Puppeth
https://modalduality.org/posts/puppeth/

Private Network
https://github.com/ethereum/go-ethereum/wiki/Private-network

Default Bootnodes
https://github.com/ethereum/go-ethereum/blob/master/params/bootnodes.go


https://alanbuxton.wordpress.com/2017/07/19/first-steps-with-ethereum-private-networks-and-smart-contracts-on-ubuntu-16-04/


https://ethereum.stackexchange.com/questions/15435/how-to-compile-solidity-contracts-with-geth-v1-6
