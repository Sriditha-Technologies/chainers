# Cryptography in Python

## Overview

Cryptography is the backbone of blockchain security, it ensures the **data integrity, authentication and confidentiality** in blockchain transactions.

## Why Cryptography important in Blockchain?

- Protects transactions from tampering
- Enables **digital signatures** in validating ownership
- Ensures secure **peer-to-peer** transactions without a central authority

## Hash functions in blockchain

### What is a hash function?

A **hash function** takes an input (string, number, or file) and returns **fixed-size** set of characters(hash). Even slight change in input creates a
**completely different hash**

### Key properties of hash function

- **Deterministic** -> Same input always provides same output
- **Fast computation** -> Quickly generates the hash
- **Pre-image Resistance** -> Hard to reverse-engineer the input from hash
- **Avalanche effect** -> A small change input drastically changes the output

**Example: SHA-256 Hashing in Python**

```python

import hashlib

data = "Blockchain security"
hashed_data = hashlib.sha256(data.encode()).hashdigest()
print(f"SHA-256 Hash: {hashed_data}")

```

**Real-world use case:** Bitcoin uses **SHA-256** to secure transactions

## Different hasing algorithms used in blockchain

| Algorithm | Used in | Hash size | Security Level |
| --------- | ------- | --------- | -------------- |
| **SHA-256** | Bitcoin, Ethereum | 256-Bit | Strong |
| **Keccak-256** | Ethereum (ETH-1.0) | 256-Bit | Strong |
| **Blake2b** | Zcash, Argon2 | 512-bit | Stronger than SHA-256 |

**Example: Using Keccak-256 (Ethereum)**

```python

import hashlib

data = "Ethereum transactions"
hashed_data = hashlib.sha3_256(data.encode()).hexdigest()
print(f"Keccak-256 Hash: {hashed_data}")

```

**Real-world use case:** **Ethereum** uses **Keccak-256** instead of SHA-256 for better efficiency

## Symmetric vs Asymmetric Cryptography

### Symmetric Cryptography

- Uses **one key** to both encrypt and decrypt data
- Example: AES (Advanced Encryption Standard)

### Asymmetric Cryptography

- Uses two keys

- **Public Key** -> Shared openly to encrypt messages
- **Private Key** -> Kept secret to decrypt messages

**Real world example:** Bitcoin wallets use asymmetric cryptography for **Secure transactions**

## Public & Private Keys in Blockchain (ECDSA)

### What is ECDSA (Explitic Curve Digital Signature Algorithm)

ECDSA is an **asymmetric cryptographic** algorithm used to:

- Generate private-public keys
- Sign and verify transactions in **Bitcoin and Ethereum**

**Example: Generating Private & Public keys in Python**

```python

from ecdsa import SigningKey, SECP256k1

# Generate private key
private_key = SigningKey.generate(curve=SECP256k1)
print(f"Private Key: {private_key.to_string().hex()}")

public_key = private_key.get_verifying_key()
print(f"Public Key: {public_key.to_string().hex()}")

```

**Real-world example:** A bitcoin wallet is generated from the public key

## Digital Signatures in Blockchain

### What is a Digital Signature

A **digital signature** ensures:
- **Authentication** -> Confirms sender identity
- **Integrity** -> Ensures data wasn't tampered with
- **Non-repudiation** -> Prevents denial of signing

**Example: Creating a digital signature**

```python

from ecdsa import SigningKey, SECP256k1

# Generate private key
private_key = SigningKey.generate(curve=SECP256k1)
message = b"Secure Blockchain Transactions"

# Sign the message
signature = private_key.sign(message)
print(f"Digital signature: {signature.hex()}")

# Verify the signature
public_key = private_key.get_verifying_key()
is_valid = public_key.verify(signature, message)
print(f"Signature is valid: {is_valid}")

```

**Real-world example:** Every bitcoin transaction is **digitally signed** for security

## Merkle Trees

### What is a Merkle Tree?

A **Merkle Tree** structures transactions in a **hierarchial** way:
- Group transactions into pairs
- Hashing each pair until one root hash remains

**Real-world use case:** Bitcoin uses Merkle Trees for efficient transaction verification

**Example: Creating a Merkle Tree**

```python

import hashlib

# Function to hash data
def hash_function(data):
    return hashlib.sha256(data.encode()).hexdigest()

# Example transactions
transactions = ["tx1", "tx2", "tx3", "tx4"]

# Hashed transactions
hashed_transactions = [hash_function(tx) for tx in transactions]

# Combine and hash pairs
while len(hashed_transactions) > 1:
    new_hashed_transactions = []
    for i in range(0, len(hashed_transactions), 2):
        combined = hashed_transactions[i] + hashed_transactions[i+1]
        new_hashed_transactions.append(hash_function(combined))
    hashed_transactions = new_hashed_transactions

# Merkle tree
print(f"Merkle root hash: {hashed_transactions[0]}")

```

**Real-world use case:** Bitcoin uses **Merkle Trees** to verify transactions without downloading the full blockchain

##Zero-Knowledge Proofs (ZKP)

### What is ZKP?

A **Zero-Knowledge Proof** allows one party to **Prove statement is true** without revealing any extra information

**Real-world use case:** Zcash uses **ZKPs** for privacy preserving transactions

### Types of ZKPs

- **zk-SNARKs** -> Used in Zcash for anonymous transactions
- **zk-STARKs** -> Faster and more scalable than zk-SNARKs
