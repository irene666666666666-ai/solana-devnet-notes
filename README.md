# Solana Devnet Notes

A short reference for checking a public wallet balance and a transaction status on Solana Devnet. Devnet is Solana's public environment for development and testing.

## Check a wallet balance

Send a JSON-RPC request to `https://api.devnet.solana.com`. Replace `YOUR_PUBLIC_WALLET_ADDRESS` with the recipient's public address.

```sh
curl -sS https://api.devnet.solana.com \
  -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"getBalance","params":["YOUR_PUBLIC_WALLET_ADDRESS",{"commitment":"finalized"}]}'
```

The response value is in lamports. Divide it by 1,000,000,000 to get SOL.

## Check a transaction

Replace `YOUR_TRANSACTION_SIGNATURE` with the signature returned by a Devnet transaction or faucet.

```sh
curl -sS https://api.devnet.solana.com \
  -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"getSignatureStatuses","params":[["YOUR_TRANSACTION_SIGNATURE"],{"searchTransactionHistory":true}]}'
```

A status of `finalized` with `err: null` indicates a successful finalized transaction. A `null` entry means the node did not return a status for that signature.

## Official references

- [Solana Devnet endpoints](https://solana.com/docs/references/clusters)
- [Solana web faucet](https://faucet.solana.com/)
- [getBalance](https://solana.com/docs/rpc/http/getbalance)
- [getSignatureStatuses](https://solana.com/docs/rpc/http/getsignaturestatuses)
