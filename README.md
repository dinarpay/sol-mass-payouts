# sol-merkle-claims

A utility allowing for mass distribution of assets, with a single
funding transaction.

## Summary example

A funder, such as a yield farming distribution, wishes to distribute
1,000,000 XYZ tokens to 50,000 addresses.

Off-chain, the funder builds a merkle tree of (address,amount) pairs for XYZ
payouts.

The funder sends 1,000,000 XYZ tokens, and the Merkle root hash, to this
MerkleBox contract for secure storage.

Then, at any time, users may claim their XYZ tokens by providing a
Merkle proof of their (address,amount).

The end result is aggregating all the payouts into a single blockchain
transaction _from the funder_.  (Users must still individually issue
claim transactions)

## Public operations (APIs)

### Anyone:  Validate claim

Validate a supplied merkle receipt is associated with a valid, unspent claim.

### User:   Claim tokens

Present a valid merkle receipt, and receive the associated tokens.

User must be the address in the claim, and the claim must be unspent.

### Funder:  Create new claims group

Store a merkle root, and associated ERC20 funds, on chain.

WARNING:  There is no on-chain validation that funds supplied equal the
funds required to fully satisfy all claims.  The funder may under-fund.

### Funder:  Add more funds to claims group.

Supply additional quantity of asset to the claims group.

### Funder:  Withdraw funds from claims group.

The funder (owner) may withdraw funds from the claims group,
if-and-only-if the "withdrawable" feature is enabled.

## Setup.
1. Install packages
   ```
   npm i -g truffle
   npm i
   ```
2. Update provider url in config/default.json
3. Set DEPLOYMENT_ACCOUNT_KEY in env
   ```
   create a .env file in root
   DEPLOYMENT_ACCOUNT_KEY =  "my mnemonic phrase"
   ```
4. Deploy you own contracts if want to do arb- 
   ``` 
   truffle migrate --reset --network mainnet/ropsten
   ```