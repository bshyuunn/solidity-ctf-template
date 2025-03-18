# foundry-ctf-template

## Getting Started
```
$ forge init --template bshyuunn/foundry-ctf-template my-solidity-challenge
$ cd my-solidity-challenge
$ make
$ nc localhost 31337
```

## Creating Your Own Challenge
To set up the environment for your challenge, simply modify the `docker-compose.yml` file. If you need to change the EVM version, make sure to update the `foundry.toml` file as well.
```yml
services:
  simple-challenge:
    build: ./build
    ports:
      - "31337:31337"
      - "8545:8545"
    restart: unless-stopped
    environment:
      - FLAG=CTF{FLAG}
      - PORT=31337
      - HTTP_PORT=8545
      - PUBLIC_IP=localhost
      - SHARED_SECRET=47066539167276956766098200939677720952863069100758808950316570929135279551683
      - ENV=production
      - SETUP_CONTRACT_VALUE=0
      - USER_VALUE=10000000000000
      - EVM_VERSION=cancun # `cancun`, `shanghai`, `paris`, `london`, etc...
```

1. **`FLAG`**  
   The secret value participants need to find.

2. **`PORT`**  
   The port for service communication (default: `31337`).

3. **`HTTP_PORT`**  
   The port for RPC communication with the Ethereum node (default: `8545`).

4. **`PUBLIC_IP`**  
   The public IP for hosting the service (set to `localhost` for local development).

5. **`SHARED_SECRET`**  
   An authentication value used when creating a blockchain network internally. (this value should be set randomly)

6. **`SETUP_CONTRACT_VALUE`**  
   The value sent to the Setup Contract (default: `0`).

7. **`USER_VALUE`**  
   The initial balance value for the CTF player.

8. **`EVM_VERSION`**  
   The Ethereum version to use (`cancun`, `shanghai`, `paris`, etc.).

Additionally, when changing the `EVM_VERSION`, make sure to update the `foundry.toml` file as well:

```toml
[profile.default]

...

evm_version = "cancun"  # Options include `cancun`, `shanghai`, `paris`, `london`, etc.
```