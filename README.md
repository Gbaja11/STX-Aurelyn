# STX-Aurelyn - Asset Smart Contract

This smart contract implements a comprehensive token system on the [Stacks blockchain](https://www.stacks.co/), written in [Clarity](https://docs.stacks.co/docs/clarity). It supports the creation, transfer, and authorization of fungible tokens, along with tracking balances, token price history, and admin-level controls.

---

## 📑 Table of Contents

* [Features](#-features)
* [Data Structures](#-data-structures)
* [Error Codes](#-error-codes)
* [Contract Initialization](#-contract-initialization)
* [Public Functions](#-public-functions)
* [Private Functions](#-private-functions)
* [Read-Only Functions](#-read-only-functions)
* [Security & Validation](#-security--validation)
* [Example Use Cases](#-example-use-cases)
* [License](#-license)

---

## 🚀 Features

* Mint new fungible tokens with metadata and price
* Track and update token prices with history
* Transfer tokens between users
* Authorize others to transfer tokens on your behalf
* Track balances and allowances
* Change contract admin securely

---

## 🗃️ Data Structures

### Maps

* `tokens`: Stores metadata for each token
* `balances`: Tracks balances of users per token
* `allowances`: Records delegated spending rights
* `price-history`: Maintains historical prices with timestamps

### Variables

* `token-counter`: Auto-incremented ID for tokens
* `contract-admin`: Owner of the contract (set at deployment)

---

## ⚠️ Error Codes

| Code   | Description                |
| ------ | -------------------------- |
| `u100` | Not authorized             |
| `u101` | Token already exists       |
| `u102` | Token not found            |
| `u103` | Insufficient funds         |
| `u104` | Invalid token name         |
| `u105` | Invalid category           |
| `u106` | Invalid max supply         |
| `u107` | Invalid token price        |
| `u108` | Invalid recipient          |
| `u109` | Invalid transfer amount    |
| `u110` | Insufficient allowance     |
| `u111` | Invalid authorized address |
| `u112` | Invalid price update       |

---

## 🛠️ Contract Initialization

When deployed, the contract sets the `contract-admin` to `tx-sender` (the deploying address).

---

## 🔓 Public Functions

### `mint-token`

Create a new token.

```clojure
(mint-token (token-name) (token-category) (max-supply) (token-price))
```

### `update-token-price`

Update token price with timestamp logging.

```clojure
(update-token-price (token-id) (new-price))
```

### `authorize-spending`

Allow another principal to spend your tokens.

```clojure
(authorize-spending (authorized) (token-id) (allowed-amount))
```

### `transfer`

Transfer tokens to another user.

```clojure
(transfer (recipient) (token-id) (transfer-amount))
```

### `transfer-as-authorized`

Authorized user transfers on behalf of token holder.

```clojure
(transfer-as-authorized (from) (recipient) (token-id) (transfer-amount))
```

### `set-contract-admin`

Change the contract admin.

```clojure
(set-contract-admin (new-admin))
```

---

## 🔒 Private Functions

### `process-transfer`

Handles internal transfer logic, adjusting balances and checking constraints.

```clojure
(process-transfer (from) (recipient) (token-id) (transfer-amount))
```

---

## 🔍 Read-Only Functions

### `get-token-details`

Get all metadata for a token.

```clojure
(get-token-details (token-id))
```

### `get-holder-balance`

Returns a user's token balance.

```clojure
(get-holder-balance (holder) (token-id))
```

### `get-authorized-amount`

Returns the remaining authorized allowance.

```clojure
(get-authorized-amount (holder) (authorized) (token-id))
```

### `get-price-at-time`

Returns the token price at a specific timestamp.

```clojure
(get-price-at-time (token-id) (timestamp))
```

---
