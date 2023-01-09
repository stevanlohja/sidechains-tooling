# Mamba CLI Reference

## Usage 

```
./mamba-cli <subcommand> <arguments...>
```

Display subcommands and options:

```shell
./mamba-cli --help
```

Display help for a specific subcommand:

```shell
./mamba-cli <subcommand> --help
```

## Commands

### `black2b`

Description: Compute `blake2b` hash. `Length` option may be `28` or `32` (default `28`)

```shell
./mamba-cli blake2b
--length <INTEGER> \
<STRING>
```

Example:

```shell
./mamba-cli blake2b \
--length 32 \
f3b12c00d0
8477c908732cda00fceb8caeaaf06de2a30175d6d3773b5443d923e1dce9fda7 #result
```

### `compress-ecdsa`

Description: Convert `ecdsa` or `eddsa` public key to its compressed version.

```shell
./mamba-cli compress-ecdsa <PUB_KEY_AS_HEX>
```

Example:

```shell
compress-ecdsa 4e38355929d3391ddf521dfffba8e52e4439a07ae18c1ccb2cfc8905c92051e2ac5975e4e15c51da7a8f58afed746b0f26e1dd80ec2ed318e64bfa95f6ea9cae
024e38355929d3391ddf521dfffba8e52e4439a07ae18c1ccb2cfc8905c92051e2 #result
```

### `create-lock-tx`

Description: Create and optionally sign lock transaction (used to transfer tokens from the SC to MC)

```shell
./mamba-cli create-lock-tx --nonce <integer> \
[--gasPrice <integer>] \
[--gasLimit <integer>] \
[--private-key <string>] \
<Recipient of the transaction on the main chain as hex> \
<Transaction amount in fuel tokens>
```

### `derive-address`

Description: Derive address from a public key.

```shell
./mamba-cli derive-address <PUB_KEY_AS_HEX>
```

Example:

```shell
./mamba-cli derive-address 4e38355929d3391ddf521dfffba8e52e4439a07ae18c1ccb2cfc8905c92051e2ac5975e4e15c51da7a8f58afed746b0f26e1dd80ec2ed318e64bfa95f6ea9cae
0x7f2891b2d56429c80bcf8649656163c92073c3a6 #result
```

### `derive-key`

Description: Derive a public key from a private one.

```shell
./mamba-cli derive-key --type <KEY_TYPE> <PRIV_KEY_AS_HEX>
```

Example:

```shell
./mamba-cli derive-key --type ecdsa cd6a22085e3e16a823a6404571b70c8dc0325efbb59ccffa2f8b24b32ad77878
{"public":"4e38355929d3391ddf521dfffba8e52e4439a07ae18c1ccb2cfc8905c92051e2ac5975e4e15c51da7a8f58afed746b0f26e1dd80ec2ed318e64bfa95f6ea9cae","publicCompressed":"024e38355929d3391ddf521dfffba8e52e4439a07ae18c1ccb2cfc8905c92051e2","address":"7f2891b2d56429c80bcf8649656163c92073c3a6"}
```

### `generate-keys`

Description: Generate key pair by type ecdsa, eddsa

```shell
./mamba-cli generate-keys --type <keyType>
```

Example:

```shell
./mamba-cli generate-keys --type ecdsa                        {"public":"4e38355929d3391ddf521dfffba8e52e4439a07ae18c1ccb2cfc8905c92051e2ac5975e4e15c51da7a8f58afed746b0f26e1dd80ec2ed318e64bfa95f6ea9cae","private":"cd6a22085e3e16a823a6404571b70c8dc0325efbb59ccffa2f8b24b32ad77878","address":"7f2891b2d56429c80bcf8649656163c92073c3a6"}
```

### `generate-signature`

Description: Compute registration signature

```shell
mamba-cli generate-signature --genesis-hash <string> \
--sidechain-id <integer | string> \
--registration-utxo <string> \
--spo-signing-key <string> \
--sidechain-signing-key <string> \
--genesis-utxo <string> \
--threshold-numerator <integer> \
--threshold-denominator <integer>
```

### `genesis-hash`

Description: Compute genesis hash.

```shell
./mamba-cli genesis-hash [--account-start-nonce <integer>] [--verbose] <genesis-file-path>
```

### `get-chain-params`

Description:  Get the chain params for a sidechain

```shell
mamba-cli get-chain-params --config-file <PATH_TO_FILE>
```

### `inspect-proof`

Description: Derive address from public key.

```shell
./mamba-cli inspect-proof [--verbose] <Serialized merkle proof as hex (in the same form as obtained from sidechain_getOutgoingTxMerkleProof endpoint)>
```

Example:

```shell
./mamba-cli inspect-proof --verbose d8799fd8799f0101581d6045736b33c53d9f526a223086afd812b07ed9741da80e989e96998893d8799f5820772485d60f6744cf252f26560413aae8d28c82a88b1c77eede792f28965f4e79ffff9fd8799f005820ed69142610619b748ec5cd657e418c1c891c3a176900376d12db0b3c406a0a38ffffff
Decoding merkle proof...
Decoded merkle proof: CombinedMerkleProof(transaction = MerkleTreeEntry(index = 1, amount = 1, recipient = 6045736b33c53d9f526a223086afd812b07ed9741da80e989e96998893, previousOutgoingTransactionsBatch = Some(772485d60f6744cf252f26560413aae8d28c82a88b1c77eede792f28965f4e79)), merkleProof = List(Up(siblingSide = Left, sibling = ed69142610619b748ec5cd657e418c1c891c3a176900376d12db0b3c406a0a38)))
{
  "merkleProof" : [
    {
      "siblingSide" : "Left",
      "sibling" : "ed69142610619b748ec5cd657e418c1c891c3a176900376d12db0b3c406a0a38"
    }
  ],
  "previousMerkleRoot" : "772485d60f6744cf252f26560413aae8d28c82a88b1c77eede792f28965f4e79",
  "transaction" : {
    "value" : 1,
    "recipient" : "6045736b33c53d9f526a223086afd812b07ed9741da80e989e96998893",
    "txIndex" : 1
  }
}
```
