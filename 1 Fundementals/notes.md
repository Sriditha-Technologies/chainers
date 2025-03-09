# Understanding Blockchain Fundementals

## What is Blockchain?

A blockchain is a decentralized, distributed digital ledger that records transactions across multiple computers. Once a transaction is recorded,
it cannot be altered, ensuring security, transparency, and immutability.

### Key features of Blockchain

- **Decentralized:** No signle entity controls it
- **Immutable:** Transactions cannot be altered or deleted
- **Transparent:** Everyone can verify the transactions
- **Secure:** Uses cryptographic hashing and consensus mechanism

**Real world example:** Bitcoin is a **Public Blockchain** where anyone can verify and send transactions without needing a bank

## How Blockchain Works?

### Structure of a blockchain

A blockchain consists of blocks, each containing:

- **Index:** Position of the block in the chain
- **Timestamp:** When the block was created
- **Transactions:** List of transactions
- **Previous Hash:** Hash of the previous block
- **Current Hash:** Unique hash for the block

**Real world example:** Think of blockchain like a linked list where each block is linked to previous one

**Example: Representing blockchain block in python**

```python

import hashlib
import time

class Block:
    def __init__(self, index, transactions, previous_hash):
        self.index = index
        self.transactions = transactions
        self.previous_hash = previous_hash
        self.timestamp = time.time()
        self.hash = self.calculate_hash()

    def calculate_hash(self):
        block_string = f"{self.index}{self.timestamp}{self.transactions}{self.previous_hash}"
        return hashlib.sha256(block_string.encode()).hexdigest()

# Example block
block = Block(1, [{"sender": "Dilip", "receiver": "Lalitha", "amount": 400}], "0")
print(f"Block hash: {block.hash}")
```

## Transactions in Blockchain

A **transaction** in blockchain consists of:

- **Sender Address:** The one who is sending the assets
- **Receiver Address:** The one who is receiving the assets
- **Amount:** The value being transferred
- **Transaction Signature:** A digital signature confirming validity

**Real world example:** When you send **Bitcoin (BTC)** or **Ethereum (ETH)**, a transaction is recorded on the blockchain

**Example: Creating a transaction in Python**

```python
import json

transaction = {
    "sender": "Dilip",
    "receiver": "Lalitha",
    "Amount": 40
}

transaction_json = json.dumps(transaction, indent=4)
print(transaction_json)
```

## Cryptographic hashing in blockchain

A hash function is used to secure blockchain data by generating a **unique fixed-length output.**

### Key properties of hashing

- **Deterministic:** Same input always produces the same output
- **Fast Computation:** Quick to generate the hash
- **Pre-image Resistance:** Cannot reverse engineer the input from hash
- **Small changes causes huge difference:** Even small input changes result in completely different hash

**Example using SHA-256 Hashing in Python**

```python

import hashlib

data = "Hello, blockchain!!!"
hashed_data = hashlib.sha256(data.encode()).hexdigest()
print(f"SHA-256 Hash: {hashed_data}")

```

**Real world example:** Bitcoin uses **SHA-256** hashing to secure transactions

## Blocks and Mining

Each **Block** in the blockchain is verified using **mining**, which is a process of solving **cryptographic** puzzles

**Proof-of-Work (PoW) Consensus**

- Miners complete to solve a complex mathematical puzzle
- The first miner to solve it gets to add a new block to the blockchain
- PoW ensures security but high computational power

**Real world example:** **Bitcoin mining** uses Proof-of-Work to validate transactions.

**Example: Simple Proof-of-Work in Python**

```python

import hashlib
import time

class Block:
    def __init__(self, index, transactions, previous_hash):
        self.index = index
        self.timestamp = time.time()
        self.transactions = transactions
        self.previous_hash = previous_hash
        self.nonce = 0 # Used for mining
        self.hash = self.calculate_hash()

    def calculate_hash(self):
        block_string = f"{self.index}{self.timestamp}{self.transactions}{self.previous_hash}{self.nonce}"
        return hashlib.sha256(block_string.encode()).hexdigest()

    def mine_block(self, difficulty):
        while self.hash[:difficulty] != "0" * difficulty:
            self.nonce += 1
            self.hash = self.calculate_hash()
        print(f"Block mined: {self.hash}")

# Simulating the mining with difficulty level 4
block = Block(1, [{"sender": "Dilip", "receiver": "Lalitha", "amount": 40}], "0")
block.mine_block(4)

```

## Public vs Private Blockchains

### Public Blockchains (Decentralized & Permissionless)

- Anyone can join and validate the transactions
- **Example:** Bitcoin, Ethereum

### Private Blockchains (Permissioned & Controlled)

- Restricted access, especially within organizations
- **Example:** Hyperledger Fabric.

**Real world example:** **Ethereum** is public, while **Hyperledger Fabric** is private, used by banks and enterprises

## Distributed Ledger Technology (DLT)

A **distributed ledger** is a database replicated across multiple nodes, ensuring:

- No signle point of failure
- Tamper-proof records
- Real-time synchronization

**Real world example:** Bank uses **DLTs** for cross-border transactions

## Use cases of Blockchain

- **Cryptocurrency** -> Bitcoin, Ethereum
- **Supply chain** -> Walmart tracks food shipments
- **Healthcare** -> Secure patient records
- **Voting systems** -> Tamper proof digital voting
- **NFTs & Gaming** -> Unique digital assets

**Real world example:** **VeChain** uses blockchain for supply chain tracking

