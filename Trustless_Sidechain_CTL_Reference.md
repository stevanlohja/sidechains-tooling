# Using Trustless Sidechain CTL

## Hardware and OS Requirements
Trustless Sidechain CTL should run on any modern OS and hardware combination capable of running a Node installation:
- Linux
- MacOS
- Windows 10+

## Prerequisites
It is assumed that you have access to:
- a shell of your choice
- NodeJS 14.20+ installed locally
- Python 3.10+ installed locally

In order to run Trustless Sidechain CTL you also need to set up the runtime dependencies:

- [ogmios](https://github.com/cardanosolutions/ogmios)
- [ogmios-datum-cache](https://github.com/mlabs-haskell/ogmios-datum-cache)
- [ctl-server](https://github.com/Plutonomicon/cardano-transaction-lib)


## Running
Extracting the distributed package produces the script `main.js` with its dependencies in `node_modules`.
It can be run from the same directory as:
```shell
node main.js <command> <options>
```

for help:
```shell
node main.js --help
```

To make multiple invocations easier, it may be desirable to export the path to your signing key: 
```bash
export SIGNING_KEY=<path to file>/server.skey
```

Available commands:

```
  init                     Initialise sidechain
  addresses                Get the script addresses for a given sidechain
  burn                     Burn a certain amount of SC_Token tokens
  claim                    Claim SC_Token from a single crsoss-chain transaction using a Merkle proof
  register                 Register a committee candidate
  deregister               Deregister a committee member
```

### Configuration
Command line arguments can be provided using a `config.json` file instead, eg.:

```json
{
  "runtimeConfig": {
    "network": null,
    "ctlServer": {
      "host": "localhost",
      "port": 8081,
      "path": null,
      "secure": false
    },
    "ogmios": {
      "host": "localhost",
      "port": 1337,
      "path": null,
      "secure": false
    },
    "ogmiosDatumCache": {
      "host": "localhost",
      "port": 9999,
      "path": null,
      "secure": false
    }
  },
  "sidechainParameters": {
    "chainId": 123, // --sidechain-id
    "genesisHash": "5f4a33beaf8876b9697fb567c9af11390434086a10454c32091e2017366dcd7a", // --sidechain-genesis-hash
    "genesisMint": null, // --genesis-mint-utxo
    "genesisUtxo": "9713f220d6d388a63fe3f426212da3af063372215e8e764c470225eab0384556#1", // --genesis-committee-hash-utxo
    "thresholdNumerator": 1, // --threshold numerator/denominator
    "thresholdDenominator": 2 // --threshold numerator/denominator
  },
  "paymentSigningKeyFile": null, // --payment-signing-key-file
  "stakeSigningKeyFile": null
}
```

### Get script addresses of a sidechain

Script addresses depend on the sidechain parameters, so we get different addresses for different parameters.
To get the script addresses for a given sidechain, you can use the following command:

```shell
node main.js -- addresses 
```

### Burn user owned SC_Token tokens

```shell
node main.js -- burn --amount 5 --recipient df7d7e053933b5cc24372f878c90e62dadad5d42
```

### Claim SC_Token

```shell
node main.js claim --payment-signing-key-file test.skey --combined-proof d8799fd8799f0002581d606e9d4f6a3f900f7b510b27f29d8e79c550686ce093946b23b3d1828ed87a80ff80ff
```

Expected output:
```json
{
  "endpoint": "ClaimAct",
  "transactionId": "1334b3dab421911af68b9393e5cc4756c46c9ab1ac567a57450597e174351a48"
}
```

### Register committee candidate

In order to generate the signatures, you can use the `sc-evm-cli` utility:

```shell
./evm-sidechain-cli generate-signature \
  --spo-signing-key 8067e0e28bbf8bf05020706074e4737b3e88554752b01b53097ebf6e267c6291 \
  --sidechain-signing-key 0046c0b086d250036896c0253e9291abc50d21bb9f445a09a8685fc09921d2bf \
  --genesis-hash d8063cc6e907f497360ca50238af5c2e2a95a8869a2ce74ab3e75fe6c9dcabd0 \
  --sidechain-id 80 \
  --genesis-utxo be6c22802e00349c953f53c2533d972accfd333e76af6dfeb2585760cdd4e933#0 \
  --threshold-numerator 2 \
  --threshold-denominator 3 \
  --registration-utxo 4f99bdb9459924e2ea2131b527c3934f0e3c2b630cea929604fd75f66fed9bcb#0
```

Example response:
```json
{
  "spoPublicKey" : "6903d409fadc11d387085a59b53770c3d6fb4c482d54b713a89a430c6987d962",
  "spoSignature" : "d61c7b893db42483fa03e574b81f599a4b27f6b77f2e6d141ead0667d31787110080b254d41def6a8e70d437caba18f3b98ab2aedf230913a356007958f58d0b",
  "sidechainPublicKey" : "023e5054a7c0d33805a845e389794c82cbf1a01f5e16b4f14ff87911bef506f1ed",
  "sidechainSignature" : "e0e87eed4b7ae50d4d0ba66adfd2ef35f5a2e08aa35dd8b75e8da17583787acf36e63a8a1b8ad7656c3919e7f2b682723fffe1fe099d113f65ac4f04596f41b7"
}
```

And use it's output for the registration:

```shell
node main.js -- register \
  --spo-public-key f71ff66b6b8da0702444183b5ce5de09f6754457a6a71b3354b81ced8dcd7e30 \
  --sidechain-public-key 03eef26d3cf978e0fc2d786c443b1284b27b265a7c82eeeec68c24cd3fd0bb6428 \
  --spo-signature 980db1db31457189326e948c7f292b16278ab91bd45f5fd6ee9ad637bf993f26936c17ee126e510c52d0a3381b52acb36a2a89d4fe55a587cf3478678114dd0f \
  --sidechain-signature bd00090a8a26b3aad534ae2e75ce4ab5b284ffad0751b793d447a3980f770f217929543c21bc7d2567c6ee0c23b983e3983f22d8eb41dfb901a6c31ae3d5b41d \
  --registration-utxo 7eddcb7807899d5078ebc25c59d372b484add88604db461e6ef077fd0379733d#0
```

### Deregister committee candidate

```shell
node main.js -- deregister \
  --payment-signing-key-file $SIGNING_KEY \
  --spo-public-key aabbcc
```

### Committee hash update

```shell
node main.js -- committee-hash \
  --committee-pub-key-and-signature aabbcc01:aaaaaa \
  --committee-pub-key-and-signature aabbcc02 \
  --committee-pub-key-and-signature aabbcc03:bbbbbb \
  --committee-pub-key-and-signature aabbcc04:cccccc \
  --new-committee-pub-key ddeeff01 \
  --new-committee-pub-key ddeeff02 \
  --new-committee-pub-key ddeeff03 \
  --new-committee-pub-key ddeeff04 \
  --sidechain-epoch 6 \
  --previous-merkle-root abcdef
```

A `--committee-pub-key-and-signature` line **must** be provided for every committee member, even if they haven't provided
a signature.

### Save merkle root

```shell
node main.js -- save-root \
  --merkle-root abababab \
  --committee-pub-key-and-signature aabbcc01:aaaaaa \
  --committee-pub-key-and-signature aabbcc02 \
  --committee-pub-key-and-signature aabbcc03:bbbbbb \
  --committee-pub-key-and-signature aabbcc04:cccccc \
  --previous-merkle-root abcdef
```

### Committee handover

```shell
node main.js -- committee-handover \
  --merkle-root abababab \
  --sidechain-epoch 6 \
  --previous-merkle-root abcdef \
  --new-committee-pub-key ddeeff01 \
  --new-committee-pub-key ddeeff02 \
  --new-committee-pub-key ddeeff03 \
  --committee-pub-key-and-new-committee-signature aabbcc01:aaaaaa \
  --committee-pub-key-and-new-committee-signature aabbcc02 \
  --committee-pub-key-and-new-committee-signature aabbcc03:bbbbbb \
  --committee-pub-key-and-new-merkle-root-signature aabbcc01:aaaaaa \
  --committee-pub-key-and-new-merkle-root-signature aabbcc02 \
  --committee-pub-key-and-new-merkle-root-signature aabbcc03:bbbbbb
```
