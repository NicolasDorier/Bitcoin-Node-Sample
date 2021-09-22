# Purpose

This is a sample docker-compose to show how to host a mainnet full-node and exposing RPC via HTTPS via a reverse proxy and let's encrypt.

1. Configure your DNS record to point the domain to the server
2. Set the environment variables.
3. Run `docker-compose up -d`

Environment variables:

`BITCOIN_HOST`: The domain name of this server. (required)
`LETSENCRYPT_EMAIL`: Email for let's encrypt (optional)
`NETWORK`: The bitcoin network (Available: mainnet,testnet,regtest,signet. Default: mainnet)
`REVERSEPROXY_HTTPS_PORT`: The port to listen to (Default 443)
`RPC_AUTH`: The RPC auth string of bitcoin core for configuring username/password

Example:

```bash
export BITCOIN_HOST="my.sampledomain.com"
docker-compose up -d
```

This should expose P2P traffic on `8333`, and RPC traffic on port `443`.