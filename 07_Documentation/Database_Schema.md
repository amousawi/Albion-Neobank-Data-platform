# Database Schema

## Core Banking Data Model

### Branches

| Column | Key Type |
|----------|----------|
| branch_code | Primary Key |
| branch_name | Attribute |
| town | Attribute |
| county | Attribute |
| region | Attribute |

---

### Customers

| Column | Key Type |
|----------|----------|
| customer_id | Primary Key |
| branch_code | Foreign Key |
| first_name | Attribute |
| last_name | Attribute |
| date_of_birth | Attribute |
| ni_number | Attribute |
| email | Attribute |
| phone_number | Attribute |
| postcode | Attribute |
| kyc_status | Attribute |

---

### Accounts

| Column | Key Type |
|----------|----------|
| account_id | Primary Key |
| customer_id | Foreign Key |
| branch_code | Foreign Key |
| account_type | Attribute |
| status | Attribute |
| balance | Attribute |
| currency | Attribute |

---

### Transactions

| Column | Key Type |
|----------|----------|
| txn_id | Primary Key |
| account_id | Foreign Key |
| txn_type | Attribute |
| amount | Attribute |
| txn_timestamp | Attribute |
| channel | Attribute |
| status | Attribute |

---

## Relationships

Branches (1) → (Many) Customers

Branches (1) → (Many) Accounts

Customers (1) → (Many) Accounts

Accounts (1) → (Many) Transactions
