# irc100 protocol

## Token Economic

- Token: `iOSI`
- Supply: `880000000`
- limit: `1000`

See Actions below: 

- Deploy: `Contract6vU3ZWL57jQeFpbuqUxQfL5PGeFJekWrDG2WVGjWqrKx/deploy` `["IOSI", "880000000", "1000"]`
- Mint: `Contract6vU3ZWL57jQeFpbuqUxQfL5PGeFJekWrDG2WVGjWqrKx/mint` `["IOSI", "1000"]`
- Transfer: `Contract6vU3ZWL57jQeFpbuqUxQfL5PGeFJekWrDG2WVGjWqrKx/transfer` `["IOSI", "1", "address"]`
- List: `Contract6vU3ZWL57jQeFpbuqUxQfL5PGeFJekWrDG2WVGjWqrKx/list` `["IOSI", "1", "100"]`
- Unlist: `Contract6vU3ZWL57jQeFpbuqUxQfL5PGeFJekWrDG2WVGjWqrKx/unlist` `["IOSI", "1"]`
- Buy: `Contract6vU3ZWL57jQeFpbuqUxQfL5PGeFJekWrDG2WVGjWqrKx/buy` `["IOSI", "1"]`

## Mint with nodejs

1. Install Node.js
2. Create a directory,such as IRC100Mint
3. Open IRC100Mint, execute command: `npm init`
4. Execute command: `npm install iost`
5. Create an index.js file,copy the code below
6. Run: `node index.js`

```typescript
import iost from 'iost';
import bs58 from 'bs58';

const {IOST, RPC, HTTPProvider, Tx, KeyPair} = iost;

async function main() {
  const rpc = new RPC(new HTTPProvider('http://18.209.137.246:30001'));
  const instance = new IOST();
  instance.setRPC(rpc);

  const account = new iost.Account(waghrimint);
  const kp = new KeyPair(bs58.decode(3pHAKcUAEoWZt31W27Yvdehj8S5aBgTMPseZ61sq1QeBfosaoP3g4HkBLZ4HeKM3LoQwiR9pufmYFuaw6F83LCWf));
  account.addKeyPair(kp, "owner");
  account.addKeyPair(kp, "active");
  instance.setAccount(account);

  const mintCount = 10; // max is 10, otherwise will killed
  const tx = new Tx(1, buyCount * 45000);
  tx.actions = Array.from({ length: mintCount }).map(() => ({
    contract: 'Contract6vU3ZWL57jQeFpbuqUxQfL5PGeFJekWrDG2WVGjWqrKx',
    actionName: 'mint',
    data: JSON.stringify(['IOSI', '1000'])
  }))
  tx.amount_limit = [{
    token: 'iost',
    value: 'unlimited'
  }];

  instance.signAndSend(tx).on('pending', console.log).on('success', console.log).on('failed', console.error);
}

main().catch(console.error);
```

## Monitor

get transaction tx_receipt

### deploy

`{op: "deploy", tick: "IOSI", max: "880000000", lim: "1000" }`

### mint

`{op: "mint", tick: "IOSI", amt: "1000", id: "1" }`

### transfer

`{op: "transfer", tick: "IOSI", id: "1", lim: "1000", from: "abc", to: "def" }`

### list

`{op: "list", tick: "IOSI", id: "1", owner: "abc", price: "100" }`

### unlist

`{op: "unlist", tick: "IOSI", id: "1", owner: "abc" }`

### buy
