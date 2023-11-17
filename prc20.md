### Deploy

|Key|Required|Description|
|---|---|---|
|p|yes|Protocol: prc-20|
|op|yes|Operation: deploy|
|tick|yes|Ticker: symbol of PRC-20 in any size and **case-insensitive**, eg. POLS = pols, max length: 18|
|max|yes|Max Supply: set max token supply, limited to uint256|
|lim|yes|Mint Limit: max amount can be minted per ordinal|
|dec|no|Decimal: decimal precision must be <=18, default to 18|

e.g.
```
{"p":"prc-20","op":"deploy","tick":"pols","max":"2100000000000000","lim":"100000000"}
```

### Mint 

|Key|Required|Description|
|---|---|---|
|p|yes|Protocol: prc-20 must be lowercase|
|op|yes|Operation: mint|
|tick|yes|Ticker: symbol of PRC-20 in any size and **case-insensitive**, eg. POLS = pols, max length: 18|
|amt|yes|mint amount , amt = lim, amt and lim must be equal|

e.g.
```
{"p":"prc-20","op":"mint","tick":"pols","amt":"100000000"}
```
Note: There cannot be any spaces or other special characters in the content of the token polscription.

### Transfer

|Key|Required|Description|
|---|---|---|
|p|yes|Protocol: prc-20 must be lowercase|
|op|yes|Operation: transfer|
|tick|yes|Ticker: symbol of PRC-20 in any size and **case-insensitive**, eg. POLS = pols, max length: 18|
|to|yes|The receiver address, and the amount to send|
|recv|yes|The receiver address|
|amt|yes|The amount to send|

e.g.
```
{"p":"prc-20","op":"transfer","tick":"pols","to":[{"recv":"0x22222222222222222222222222222222222222222222","amt":"1000000"}]}
```

### Procy Transfer 
pending
### Freeze Sell
pending

## Detailed examples

```js
// data:application/json,
// +

// deploy; send 0eth from self to 0x0000000000000000000000000000000000000000;
{
    "p":"prc-20", //protocol name: prc20 | prc-20
    "op":"deploy", //operation: deploy/mint/transfer/freeze_sell/proxy_transfer
    "tick":"pols", //token tick, can't be repeatable, case insensitive.
    "max":"2100000000000000", //max supply
    "lim":"100000000", //limit for each mint
    "wlim":"10000000", //limit for each address can maximum mint, address balance < deploy.wlim (Before mint, please do not receive transfers from others, transfers are also counted as balance)
    "dec":"8", //decimal for minimum divie
}

// mint; send 0eth from self to 0x0000000000000000000000000000000000000000;
// The initiator of the transaction is the receiver
{
    "p":"proc-20",
    "op":"mint", //mint operation
    "tick":"pols",
    "amt":"100000000", //mint amount
}

// transfer; send 0eth from self to 0x0000000000000000000000000000000000000000
{
  "p": "prc-20",
  "op": "transfer", //transfer operation
  "tick": "pols",
  "to": [ //batch transfer, the sum of amt must equal the previous amt param
    {
      "recv": "0x22222222222222222222222222222222222222222222", //receiver address
      "amt": "50000000" //receiver amount
    },
    {
      "recv": "0x33333333333333333333333333333333333333333333",
      "amt": "50000000"
    }
  ]
}
// proxy transfer; send 0eth from self to 0x0000000000000000000000000000000000000000 or platform address
pending
// The buyer is buying and the seller's token is frozen;  send x eth from self to 0x0000000000000000000000000000000000000000 or platform address
pending

// cancel approve; send 0eth from self to 0x0000000000000000000000000000000000000000
{
  "p": "prc-20",
  "op": "cancel_approve",
  "sign": [
    {
        "message": "",
        "sign": "0xsign"
    }
  ]
}
```