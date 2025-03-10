# Setting up Python for Blockchain Development

## Overview

Before we start building blockchain applications, we need to setup our **development environment** properly, in this section we will:

- Install essential **Python libraries** for blockchain development
- Setup **FastAPI** for a RESTful blockchain API
- Connect to **Ethereum blockchain using web3.py**
- Setup **PostgreSQL and MongoDB** for storing blockchain data

## Installing required Python libraries

### Key libraries for blockchain development

| Library | Purpose |
| ------- | ------- |
| web3.py | Connects Python to Ethereum Blockchain |
| cryptography | Handles encryption, digital signatures |
| flask/FastAPI | Builds APIs for blockchain transactions |
| requests | Fetches blockchain data from APIs |
| pydantic | Validates blockchain transaction data |
| sqlalchemy | Handles postgresql database storage |
| pymongo | Manages MongoDB storage |
| alembic | Manages postgresql database migrations |

### Installing all dependencies

Run the following command to install everything at once

```bash
pip install web3 cryptography flask fastapi requests pydantic sqlalchemy alembic greenlet pymongo uvicorn
```

## Setting up a FastAPI Blockchain API

### What is FastAPI?

FastAPI is a **high performance web framework** used for building **blockchain REST APIs**

### Step1: Creating a FastAPI project
```bash
mkdir blockchain-api & cd blockchain-api
python -m venv venv
source venv/bin/activate # MacOS/Linux
venv\Scripts\Activate # Windows
pip install fastapi uvicorn
```

### Step2: Creating main.py for FastAPI
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"message": "Welcome to Blockchain API"}

# Run the server using command uvicorn main:app --reload
```

### Run API Server
```bash
uvicorn main:app --reload
```

Open in browser: **http://localhost:8000**

**Real-world use case** Every blockchain API needs an API to **Submit Transactions** and fetch **Blockchain data**

## Connecting to **Ethereum** blockchain using Web3.py

### What is web3.py?

**web3.py** is a library that allows us to:
- Read blockchain data (blocks, transactions)
- Send transactions (transfer ETH, interact with smart contracts)

### Step 1: Install web3.py
```bash
pip install web3
```



