# Sidechain CLI Reference

## Usage 

```
./sidechain-cli <subcommand> <arguments...>
```
## Prequisites
It is assumed that you have access to:
- a shell of your choice
- [Java](http://www.java.com/getjava/) 14.20+ installed locally 
- [Node.js](https://nodejs.org/en/download/) V10 or later
- [Python](https://www.python.org/downloads/) V3.5 or later
## Commands

### `request-funds`

Description: Request funds for a sidechain recipient address.

```
./sidechain-cli request_funds
  --sc-url <RPC_URL> \
  --recipient <SC_ADDRESS>
```

Example:

```
./sidechain-cli request-funds
  --sc-url http://localhost:8546 \
  --recipient ae3dffee97f92db0201d11cb8877c89738353bce
```

### `burn-fuel`

Description: Send SC_Token tokens from mainchain to sidechain recipient address.

```
./sidechain-cli burn-fuel
  --signing-key-file <PATH_TO_FILE>.skey \
  --sc-url <SC_RPC_URL>\
  --recipient <SC_ADDRESS>\
  --amount <INTEGER>
```

Example:

```
./sidechain-cli burn-fuel
  --signing-key-file payment.skey \
  --sc-url http://localhost:8546 \
  --recipient ae3dffee97f92db0201d11cb8877c89738353bce \
  --amount 10
```

### `search-incoming-txs`

Description: Search sidechain for transactions from mainchain to sidechain. Reads the chain backward and prints transaction that matches the filters.

```
./sidechain-cli search-incoming-txs
  --from <START_BLOCK_NUM> \
  --to <END_BLOCK_NUM> \
  --sc-url <SC_RPC_URL> \
  --recipient <SC_ADDRESS> \ #optional recipient sidechain address
  --utxo-id <MN_UTXO_ID> #optional mainchain tx ID
```

Example:

```
./sidechain-cli search_incoming_txs
  --from 210000 \
  --to 209500 \
  --sc-url http://localhost:8546
```

### `claim-fuel`

Description: Claim SC_Token tokens that have been sent from sidechain to mainchain using obtained merkle proof.

```
./sidechain-cli claim-fuel
  --signing-key-file <PATH_TO_FILE> \ 
  --sc-url <RPC_URL> \
  --combined-proof <MERKLE_PROOF_BYTES>

```


Example:

```
./sidechain-cli claim-fuel
  --signing-key-file payment.skey \ 
  --sc-url http://localhost:8546 \
  --combined-proof d8799fd8799f0101581d6045736b33c53d9f526a223086afd812b07ed9741da80e989e96998893d8799f5820772485d60f6744cf252f26560413aae8d28c82a88b1c77eede792f28965f4e79ffff9fd8799f005820ed69142610619b748ec5cd657e418c1c891c3a176900376d12db0b3c406a0a38ffffff
```

### `pending-txs`

Description: Displays pending and queued transactions from mainchain to sidechain

```
./sidechain-cli pending-txs
  --sc-url <SC_RPC_URL> \
  --recipient <SC_ADDRESS>
```


