# Sidechain EVM CLI Reference

## Usage

```shell
./sc-evm-cli <subcommand> <arguments...>
```

Display subcommands and options:

```shell
./sc-evm-cli --help
```

Display help for a specific subcommand:

```shell
./sc-evm-cli <subcommand> --help
```

## Commands

### `generate-signature`

Description: Compute registration signature

```shell
sc-evm-cli generate-signature --genesis-hash <string> \
--sidechain-id <integer | string> \
--registration-utxo <string> \
--genesis-utxo <string> \
--threshold-numerator <integer> \
--threshold-denominator <integer> \
--spo-signing-key <string> \
--sidechain-signing-key <string>
```
