# Aptos Starter

**Initialize local configuration and create an account**

The `aptos init` command will initialize the configuration with the private key you provided.

```powershell
$ aptos init
Configuring for profile default
Enter your rest endpoint [Current: None | No input: https://fullnode.devnet.aptoslabs.com]

No rest url given, using https://fullnode.devnet.aptoslabs.com...
Enter your faucet endpoint [Current: None | No input: https://faucet.devnet.aptoslabs.com]

No faucet url given, using https://faucet.devnet.aptoslabs.com...
Enter your private key as a hex literal (0x...) [Current: None | No input: Generate new key (or keep one if present)]

No key given, generating key...
Account 00f1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696 doesn't exist, creating it and funding it with 10000 coins
Aptos is now set up for account 00f1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696!  Run `aptos help` for more information about commands

{
  "Result": "Success"
}
```

**Creating other profiles**

by using --profile argument you can also create other profiles for different endpoints and different keys.

```powershell
$ aptos init --profile superuser
Configuring for profile superuser
Enter your rest endpoint [Current: None | No input: https://fullnode.devnet.aptoslabs.com]

No rest url given, using https://fullnode.devnet.aptoslabs.com...
Enter your faucet endpoint [Current: None | No input: https://faucet.devnet.aptoslabs.com]

No faucet url given, using https://faucet.devnet.aptoslabs.com...
Enter your private key as a hex literal (0x...) [Current: None | No input: Generate new key (or keep one if present)]

No key given, generating key...
Account 18B61497FD290B02BB0751F44381CADA1657C2B3AA6194A00D9BC9A85FAD3B04 doesn't exist, creating it and funding it with 10000 coins
Aptos is now set up for account 18B61497FD290B02BB0751F44381CADA1657C2B3AA6194A00D9BC9A85FAD3B04!  Run `aptos help` for more information about commands
{
  "Result": "Success"
}
```

## Account examples[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#account-examples)

### Fund an account with the faucet

```powershell
$ aptos account fund-with-faucet --account 00f1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696
{
  "Result": "Added 10000 coins to account 00f1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696"
}
```

**View an account's balance and transfer events[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#view-an-accounts-balance-and-transfer-events)**

```powershell
$ aptos account list --query balance --account 00f1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696
```

it will display following command

```powershell
{
  "Result": [
    {
      "coin": {
        "value": "110000"
      },
      "deposit_events": {
        "counter": "3",
        "guid": {
          "id": {
            "addr": "0xf1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696",
            "creation_num": "2"
          }
        }
      },
      "frozen": false,
      "withdraw_events": {
        "counter": "0",
        "guid": {
          "id": {
            "addr": "0xf1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696",
            "creation_num": "3"
          }
        }
      }
    }
  ]
}
```

**Listing resources in an account[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#listing-resources-in-an-account)**

```powershell
$ aptos account list --query resources --account 0xf1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696
```

it will generate

```powershell
{
  "Result": [
    {
      "0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>": {
        "coin": {
          "value": "110000"
        },
        "deposit_events": {
          "counter": "3",
          "guid": {
            "id": {
              "addr": "0xf1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696",
              "creation_num": "2"
            }
          }
        },
        "frozen": false,
        "withdraw_events": {
          "counter": "0",
          "guid": {
            "id": {
              "addr": "0xf1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696",
              "creation_num": "3"
            }
          }
        }
      }
    },
    {
      "0x1::account::Account": {
        "authentication_key": "0x00f1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696",
        "coin_register_events": {
          "counter": "1",
          "guid": {
            "id": {
              "addr": "0xf1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696",
              "creation_num": "0"
            }
          }
        },
        "guid_creation_num": "4",
        "key_rotation_events": {
          "counter": "0",
          "guid": {
            "id": {
              "addr": "0xf1f20ddd0b0dd2291b6e42c97274668c479bca70f07c6b6a80b99720779696",
              "creation_num": "1"
            }
          }
        },
        "rotation_capability_offer": {
          "for": {
            "vec": []
          }
        },
        "sequence_number": "0",
        "signer_capability_offer": {
          "for": {
            "vec": []
          }
        }
      }
    }
  ]
}
```

**Compiling Move**

The named addresses can be either an account address, or a profile name.

```powershell
$ aptos move compile --package-dir aptos-move/move-examples/hello_blockchain/ --named-addresses hello_blockchain=superuser
```

It will generate following output

```powershell
{
  "Result": [
    "742854F7DCA56EA6309B51E8CEBB830B12623F9C9D76C72C3242E4CAD353DEDC::Message"
  ]
}
```

**Compiling and unit testing Move[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#compiling-and-unit-testing-move)**

```powershell
$ aptos move test --package-dir aptos-move/move-examples/hello_blockchain/ --named-addresses hello_blockchain=superuser
```

It will generate following output

```powershell
INCLUDING DEPENDENCY AptosFramework
INCLUDING DEPENDENCY AptosStdlib
INCLUDING DEPENDENCY MoveStdlib
BUILDING Examples
Running Move unit tests
[ PASS    ] 0x742854f7dca56ea6309b51e8cebb830b12623f9c9d76c72c3242e4cad353dedc::MessageTests::sender_can_set_message
[ PASS    ] 0x742854f7dca56ea6309b51e8cebb830b12623f9c9d76c72c3242e4cad353dedc::Message::sender_can_set_message
Test result: OK. Total tests: 2; passed: 2; failed: 0
{
  "Result": "Success"
}
```

**Publishing a Move package with a named address[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#publishing-a-move-package-with-a-named-address)**

```powershell
$ aptos move publish --package-dir aptos-move/move-examples/hello_blockchain/ --named-addresses HelloBlockchain=8946741e5c907c43c9e042b3739993f32904723f8e2d1491564d38959b59ac71
```

**Running a Move function**

```powershell
$ aptos move run --function-id 0xb9bd2cfa58ca29bce1d7add25fce5c62220604cd0236fe3f90d9de91ed9fb8cb::message::set_message --args string:hello!
{
  "Result": {
    "changes": [
      {
        "address": "b9bd2cfa58ca29bce1d7add25fce5c62220604cd0236fe3f90d9de91ed9fb8cb",
        "data": {
          "authentication_key": "0xb9bd2cfa58ca29bce1d7add25fce5c62220604cd0236fe3f90d9de91ed9fb8cb",
          "self_address": "0xb9bd2cfa58ca29bce1d7add25fce5c62220604cd0236fe3f90d9de91ed9fb8cb",
          "sequence_number": "3"
        },
        "event": "write_resource",
        "resource": "0x1::account::Account"
      },
      {
        "address": "b9bd2cfa58ca29bce1d7add25fce5c62220604cd0236fe3f90d9de91ed9fb8cb",
        "data": {
          "coin": {
            "value": "9777"
          },
          "deposit_events": {
            "counter": "1",
            "guid": {
              "id": {
                "addr": "0xb9bd2cfa58ca29bce1d7add25fce5c62220604cd0236fe3f90d9de91ed9fb8cb",
                "creation_num": "1"
              }
            }
          },
          "withdraw_events": {
            "counter": "1",
            "guid": {
              "id": {
                "addr": "0xb9bd2cfa58ca29bce1d7add25fce5c62220604cd0236fe3f90d9de91ed9fb8cb",
                "creation_num": "2"
              }
            }
          }
        },
        "event": "write_resource",
        "resource": "0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>"
      },
      {
        "address": "b9bd2cfa58ca29bce1d7add25fce5c62220604cd0236fe3f90d9de91ed9fb8cb",
        "data": {
          "counter": "4"
        },
        "event": "write_resource",
        "resource": "0x1::guid::Generator"
      },
      {
        "address": "b9bd2cfa58ca29bce1d7add25fce5c62220604cd0236fe3f90d9de91ed9fb8cb",
        "data": {
          "message": "hello!",
          "message_change_events": {
            "counter": "0",
            "guid": {
              "id": {
                "addr": "0xb9bd2cfa58ca29bce1d7add25fce5c62220604cd0236fe3f90d9de91ed9fb8cb",
                "creation_num": "3"
              }
            }
          }
        },
        "event": "write_resource",
        "resource": "0xb9bd2cfa58ca29bce1d7add25fce5c62220604cd0236fe3f90d9de91ed9fb8cb::Message::MessageHolder"
      }
    ],
    "gas_used": 41,
    "success": true,
    "version": 3488,
    "vm_status": "Executed successfully"
  }
}
```

## Node command examples[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#node-command-examples)

### Running a local testnet

You can run a local testnet from the aptos CLI, that will match the version it was built with. Additionally, it can run a faucet side by side with the local single node testnet.

```powershell
$ aptos node run-local-testnet --with-faucet
Completed generating configuration:
        Log file: "/Users/greg/.aptos/testnet/validator.log"
        Test dir: "/Users/greg/.aptos/testnet"
        Aptos root key path: "/Users/greg/.aptos/testnet/mint.key"
        Waypoint: 0:d302c6b10e0fa68bfec9cdb383f24ef1189d8850d50b832365eea21ae52d8101
        ChainId: TESTING
        REST API endpoint: 0.0.0.0:8080
        Fullnode network: /ip4/0.0.0.0/tcp/6181

Aptos is running, press ctrl-c to exit
```

This will have consistent state if the node is shutdown, it will start with the previous state. If you want to restart the chain from genesis, you can add the `--force-restart`
 flag.

```powershell
$ aptos node run-local-testnet --with-faucet --force-restart
Are you sure you want to delete the existing chain? [yes/no] >
yes
Completed generating configuration:
        Log file: "/Users/greg/.aptos/testnet/validator.log"
        Test dir: "/Users/greg/.aptos/testnet"
        Aptos root key path: "/Users/greg/.aptos/testnet/mint.key"
        Waypoint: 0:649efc34c813d0db8db6fa5b1ffc9cc62f726bb5168e7f4b8730bb155d6213ea
        ChainId: TESTING
        REST API endpoint: 0.0.0.0:8080
        Fullnode network: /ip4/0.0.0.0/tcp/6181

Aptos is running, press ctrl-c to exit
```

### Prepare aptos-core[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#prepare-aptos-core)

The following guide assumes that you have access to the Aptos-core repository or the associated tools.

```powershell
git clone https://github.com/aptos-labs/aptos-core.git
cd aptos-core
git checkout --track origin/testnet
./scripts/dev_setup.sh
source ~/.cargo/env
```

### The `layout` file[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#the-layout-file)

The layout file contains:

- `root_key`: an Ed25519 public key for AptosCoin management.
- `users`: the set of participants
- `chain_id`: the `ChainId` or a unique integer that distinguishes this deployment from other Aptos networks

An example:

```powershell
root_key: "0xca3579457555c80fc7bb39964eb298c414fd60f81a2f8eedb0244ec07a26e575"
users:
  - alice
  - bob
chain_id: 8
```

### Building the Aptos Framework[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#building-the-aptos-framework)

From your Aptos-core repository, build the framework and package it:

```
cargo run --package framework
mkdir aptos-framework-release
cp aptos-framework/releases/artifacts/current/build/**/bytecode_modules/* aptos-framework-release

```

The framework will be stored within the `aptos-framework-release` directory.

### The `ValidatorConfiguration` file[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#the-validatorconfiguration-file)

The `ValidatorConfiguration` file contains:

- `account_address`: The account that manages this validator. This must be derived from the `account_key` provided within the `ValidatorConfiguration` file.
- `consensus_key`: The public key for authenticating consensus messages from the validator
- `account_key`: The public key for the account that manages this validator. This is used to derive the `account_address`.
- `network_key`: The public key for both validator and fullnode network authentication and encryption.
- `validator_host`: The network address where the validator resides. This contains a `host` and `port` field. The `host` should either be a DNS name or an IP address. Currently only IPv4 is supported.
- `full_node_host`: An optional network address where the fullnode resides. This contains a `host` and `port` field. The `host` should either be a DNS name or an IP address. Currently only IPv4 is supported.
- `stake_amount`: The number of coins being staked by this node. This is expected to be `1`, if it is different the configuration will be considered invalid.

An example:

```
account_address: ccd49f3ea764365ac21e99f029ca63a9b0fbfab1c8d8d5482900e4fa32c5448a
consensus_key: "0xa05b8f41057ac72f9ca99f5e3b1b787930f03ba5e448661f2a1fac98371775ee"
account_key: "0x3d15ab64c8b14c9aab95287fd0eb894aad0b4bd929a5581bcc8225b5688f053b"
network_key: "0x43ce1a4ac031b98bb1ee4a5cd72a4cca0fd72933d64b22cef4f1a61895c2e544"
validator_host:
  host: bobs_host
  port: 6180
full_node_host:
  host: bobs_host
  port: 6182
stake_amount: 1

```

To generate this using the `aptos` CLI:

1. Generate your validator's keys:

```
cargo run --package aptos -- genesis generate-keys --output-dir bobs

```

1. Generate your `ValidatorConfiguration`:

```
cargo run --package aptos -- \\
    genesis set-validator-configuration \\
    --keys-dir bobs \\
    --username bob \\
    --validator-host bobs_host:6180 \\
    --full-node-host bobs_host:6180 \\
    --local-repository-dir .

```

1. The last command will produce a `bob.yaml` file that should be distributed to other participants for `genesis.blob` generation.

### Generating a genesis and waypoint[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#generating-a-genesis-and-waypoint)

`genesis.blob` and the waypoint can be generated after obtaining the `Layout` file, each of the individual `ValidatorConfiguration` files, and the framework release. It is important to validate that the `ValidatorConfiguration` provided in the earlier stage is the same as in the distribution for generating the `genesis.blob`. If there is a mismatch, inform all participants.

To generate the `genesis.blob` and waypoint:

- Place the `Layout` file in a directory, e.g., `genesis`.
- Place all the `ValidatorConfiguration` files into the `genesis` directory.
- Ensure that the `ValidatorConfiguration` files are listed under the set of `users` within the `Layout` file.
- Make a `framework` directory within the `genesiss` directory and place the framework release `.mv` files into the `framework` directory.
- Use the `aptos` CLI to generate genesis and waypoint:

```
cargo run --package aptos -- genesis generate-genesis --local-repository-dir genesis

```

### Starting an `aptos-node`[](https://aptos.dev/cli-tools/aptos-cli-tool/use-aptos-cli#starting-an-aptos-node)

Upon generating the `genesis.blob` and waypoint, place them into your validator and fullnode's configuration directory and begin your validator and fullnode.