# WC JSON-RPC for Everscale
### Common response model
```
{
    "data": dict | null,
    "error": string | null
}
```
### ever_getAccounts
Returns a list of all wallet addresses available for all methods of this JSON-RPC. 


##### Parameters:
not

##### Returns:
1. accounts: list[Account]

    Account - dictionary:
   1. address - owner's wallet address
##### Example:
```
// Request
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "ever_getAccounts",
  "params": {}
}
 
// Result
{
  "id": 1,
  "jsonrpc": "2.0",
  "result":  {
        "data": [
             { "address": "0:b38d96bceaa156c07f22b5596c2374b87e26cc53b1b6d7df43401d671bdea708" },
             { "address": "0:695e425fc721b988f86268062fbb1b812d792ee544f2abeb3b772cc1e579db8d" }
        ],
        "error": null
    }
}
```
### ever_processMessage
Creates message, sends it to the network and monitors its processing.
##### Parameters:
1. address - string, wallet address received from "ever_getAccounts"
2. method - string, method of smartcontract
3. method_params -  dictionary, method params of smartcontract
##### Returns:
1. out_msgs  - list[string], list of output messages ids
##### Example:
```
// Example for MultisigWallet
// Request
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "ever_processMessage",
  "params": {
        "address": "0:695e425fc721b988f86268062fbb1b812d792ee544f2abeb3b772cc1e579db8d"
        "method": "sendTransaction",
        "method_params": {
            "dest": "0:b38d96bceaa156c07f22b5596c2374b87e26cc53b1b6d7df43401d671bdea708",
            "value": 1000000000,
            "bounce": False,
            "flags": 0,
            "payload": ""
        },
    }
}
 
// Result
{
  "id": 1,
  "jsonrpc": "2.0",
  "result":  {
        "data": {
            "out_msgs": ["c0b0996a9f0ea8e472041857ff2da9cf8086a78603f823a7170891f43a217ff1"]
        },
        "error": null
    }
}
```
