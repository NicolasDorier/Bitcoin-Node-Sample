# Purpose

This is a sample docker-compose to show how to host a mainnet full-node and exposing RPC via HTTPS via a reverse proxy and let's encrypt.

1. Configure your DNS record to point the domain to the server
2. Set the environment variables.
3. Run `docker-compose up -d`

Environment variables:

* `BITCOIN_HOST`: The domain name of this server. (required)
* `LETSENCRYPT_EMAIL`: Email for let's encrypt (optional)
* `NETWORK`: The bitcoin network (Available: mainnet,testnet,regtest,signet. Default: mainnet)
* `REVERSEPROXY_HTTPS_PORT`: The port to listen to (Default 443)
* `RPC_AUTH`: The RPC auth string of bitcoin core for configuring username/password

Example:

```bash
rm -f .env
# Setup rpc user/password
RPC_USER="testuser"
RPC_PASS="testpass"
# Setup the domain name
BITCOIN_HOST="my.sampledomain.com"
NETWORK="mainnet"

echo "RPC_AUTH=$(./rpcauth.py $RPC_USER $RPC_PASS | grep rpcauth)" >> .env
echo "BITCOIN_HOST=$BITCOIN_HOST" >> .env
echo "NETWORK=$NETWORK" >> .env

docker-compose up -d
```

You can also use a .env file in this folder.

This should expose P2P traffic on `8333`, and RPC traffic on port `443`.

You can use RPC of the node via the `bitcoin-cli.sh` script.

```bash
./bitcoin-cli.sh getblockchaininfo
```