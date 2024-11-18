# Important concepts
- Async cryptography: signature (secret sign, public verify), decryption (public encrypt, secret decrypt)
- Public key as address
- Decentralization, validator nodes
- Hashing & chaining
- Token: fungible vs non-fungible (ownership, identity case), created by projects
- Smart contract: code uploaded to blockchain -> dApp
- Transaction: add to the chain, atomic
- Wallet: store private keys locally
- Solana: efficiency, performance, cost, reliability issues, growth, SOL coin
- Explorer: https://explorer.solana.com/?cluster=devnet

# Solana APIs
- Web3 js: client lib? Interact with Solana APIs
- Connect to dev-test/main-beta cluster
- Address look up
- Get acc balance using public key
- Transaction:
  - Set of instructions
  - Instruction:
    - Accounts
    - Public key of program to run (system vs custom?)
    - Program args
  - Atomic
  - Written to a block
  - Fee
- Wallet:
  - 2 parts: wallet app & FE app using wallet client lib
  - Mechanism: wallet app inject script to browser run time -> FE app invokes the script -> connect -> sign txn -> FE app executes txn
