# Sending Messages Using Foundry

In the previous section, we have seen how to send messages using Remix. In this section, we will show how to send messages using [Foundry](https://book.getfoundry.sh/).

## Overview

This example is based on a basic [Counter](https://github.com/msgport/msgport-examples/blob/main/src/counter/src/Counter.sol) smart contract. The contract is simple and easy to understand. A contract with a `number` storage is deployed in the Sepolia testnet, and another contract named [CounterSender](https://github.com/msgport/msgport-examples/blob/main/src/counter/src/CounterSender.sol) is deployed in the [Koi testnet](https://docs.darwinia.network/build/getting-started/networks/koi/). The goal is to call the `increaseNumber()` function of the Sepolia Counter from the Koi testnet CounterSender.

## Preparation

### Clone repo and submodules

```bash
git clone --recursive https://github.com/msgport/msgport-examples.git
cd msgport-examples
```

### Account with balance

Before proceeding with the tutorial, you need an account with sufficient balance. This is required to perform contract operations in both the [Koi](https://docs.darwinia.network/build/getting-started/networks/koi/) and Sepolia testnets. If you don't have an account with sufficient balance, you may encounter difficulties when interacting with these contracts. Once you have the account, copy and create a `.env` file based on the `.env.example` file in the root of the repository. This will allow you to continue with the tutorial.

### Deploy Counter in the Sepolia testnet

Running the script to deploy the `Counter` contract in the Sepolia testnet:

```bash
forge script src/counter/script/Deploy.s.sol:DCounter --broadcast --rpc-url https://ethereum-sepolia.publicnode.com
```

The output:

```bash
Script ran successfully.                                                                                                                                                           
== Logs ==                                                                                                                                         
  Counter has been deployed at chain: 11155111, contract: 0xc2fEFb4FDC7E6CaB6FaC7cb3A83902Aea0cB0348                                                           
  
## Setting up 1 EVM.            

==========================                                                                                                                 

Chain 11155111                                                                                                                                                 
Estimated gas price: 0.055286148 gwei                                                                                                                          
Estimated total gas used for script: 214358                                                                                                                                     
Estimated amount required: 0.000011851028112984 ETH                            
==========================                                                                                                                                                                                                                                                            
##### sepolia                                                                                                                                                                      
✅  [Success]Hash: 0xe866afcca912979c531b5100876c3e86315d9a641dcf232c5c95b702e220fe51                                                                                                                                                                                                                                        
Contract Address: 0xc2fEFb4FDC7E6CaB6FaC7cb3A83902Aea0cB0348                                                                                                   
Block: 6138758                                                                 
Paid: 0.00000868981192167 ETH (164935 gas * 0.052686282 gwei)                  
✅ Sequence #1 on sepolia | Total Paid: 0.00000868981192167 ETH (164935 gas * avg 0.052686282 gwei) 
```

### Check the initial number value

Once the `Counter` has been deployed, we can check the current `number` stored in the Counter.

```bash
forge script src/counter/script/GetNumber.s.sol:GetNumber --rpc-url https://ethereum-sepolia.publicnode.com 
```

The output:

```bash
The current number stored in the Counter is: 0
```

### Deploy CounterSender in the Koi testnet 

Running the script to deploy the `CounterSender` contract in the Koi testnet:

```bash
forge script src/counter/script/Deploy.s.sol:DCounterSender --broadcast --rpc-url https://koi-rpc.darwinia.network
```

The output:

```bash
[⠊] Compiling...                                                               
[⠔] Compiling 28 files with Solc 0.8.21                                                                                                                                                                                                                                                                                       
[⠒] Solc 0.8.21 finished in 3.40s                                              
Compiler run successful with                                                                                                                        
Script ran successfully.                                                                                                                                                                                                                                                                                                      
== Logs ==                                                                     
  Sender has been deployed at chain: 701, contract: 0x36d95D59391e202b44B37d5599a119C1b718efB1
                                                                                                                                                               
## Setting up 1 EVM.                                                                                                                                                                                                                                                                                                          
==========================                                                                                                                                                                                                                                                                                                    
Chain 701                                                                      
                                                                               
Estimated gas price: 150.706512128 gwei                                        
Estimated total gas used for script: 272867                                                                                                                                                                                                                                                                                   
Estimated amount required: 0.041122833844830976 ETH                            
==========================                                                                                                                                     
##### 701                                                                                                                                                      
✅  [Success]Hash: 0xb3985ea1d6b8d9795d829684ef3a0f098e8eab8a45f2d5f65e1256d2e3818e1e
Contract Address: 0x36d95D59391e202b44B37d5599a119C1b718efB1                                                                                                   
Block: 97100                                                                                                                                                   
Paid: 0.015820717523661056 ETH (209954 gas * 75.353256064 gwei)                
```
### Send Message from the Koi testnet to the Sepolia testnet

```bash
forge script src/counter/script/IncreaseNumber.s.sol:IncreaseNumber -vv --broadcast --rpc-url https://koi-rpc.darwinia.network --gas-estimate-multiplier 200
```

The output:

```bash
Script ran successfully.                                                       
                                                                               
== Logs ==                                                                                                                                                     
  the body is: {"fromAddress":"0x36d95D59391e202b44B37d5599a119C1b718efB1","fromChainId":701,"message":"0x5b4ef819","ormp":{"refundAddress":"0x0000000000000000000000000000000000000000"},"toAddress":"0xea02E187B97622Ca74c58107236b0182CE727b70","toChainId":11155111}                                                      
  The message has been sent to chain: 11155111, msgId: 0xec7358b1570f5b23dee8a732ece84970e8ab9c349f610440a38c07a5fcd3a772
                                                                               
## Setting up 1 EVM.                                                           
==========================                                                     
Chain 701                                                                                                                                                      
Estimated gas price: 150.706512128 wei                                                                                                                        
Estimated total gas used for script: 264208
Estimated amount required: 0.039817866156314624 ETH

==========================

##### 701
✅  [Success]Hash: 0x5a9c8e8150391fd0eee27b8f78128d07fb6c806cc12ff60c220c586daef20a1e
Block: 97272
Paid: 0.013607441686549248 ETH (180582 gas * 75.353256064 gwei)

✅ Sequence #1 on 701 | Total Paid: 0.013607441686549248 ETH (180582 gas * avg 75.353256064 gwei)
```

After submitting the transaction, you have successfully sent a message from the Koi testnet to the Sepolia testnet. Please wait for the message to be delivered and dispatched in the Sepolia testnet. 

The msgId `0xec7358b1570f5b23dee8a732ece84970e8ab9c349f610440a38c07a5fcd3a772` is the unique identifier of the message, you can track the message status in the [Msgport Scan](https://scan.msgport.xyz/). It usually takes less than 5 minutes. Once the message status turns from `Inflight` to `Success`, you can check the `number` value again in the Sepolia testnet.

### Check the number again

```bash
forge script src/counter/script/GetNumber.s.sol:GetNumber --rpc-url https://ethereum-sepolia.publicnode.com 
```

The output:

```bash
The current number stored in the Counter is: 1
```