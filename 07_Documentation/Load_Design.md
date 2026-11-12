# Load Design

## Overview

The Albion NeoBank platform will implement a Medallion Architecture consisting of Bronze, Silver and Gold layers.

Data will be loaded incrementally from source files stored in the Databricks managed volume.

---

## Source Layer

Source files are stored within:

albion.default.albion_source_files

Supported formats:

- CSV
- JSONL

Source systems:

- Customers
- Accounts
- Branches
- Transactions
- CRA
- Checkout.com
- Worldpay
- Adyen
- Stripe

---

## Bronze Layer

Purpose:

Store raw source data with minimal transformation.

Processing:

- Read source files
- Add ingestion timestamp
- Add source system name
- Add batch identifier
- Preserve original data

Output:

bronze_customers

bronze_accounts

bronze_branches

bronze_transactions

bronze_cra

bronze_checkoutcom

bronze_worldpay

bronze_adyen

bronze_stripe

---

## Silver Layer

Purpose:

Store cleansed and validated data.

Processing:

- Type conversion
- Duplicate removal
- Null validation
- Business rule validation
- Standardised formats

Output:

silver_customers

silver_accounts

silver_branches

silver_transactions

silver_payments

---

## Gold Layer

Purpose:

Provide business-ready datasets.

Processing:

- Aggregation
- KPI calculations
- Reporting datasets
- Dashboard datasets

Output:

gold_customer_summary

gold_account_summary

gold_transaction_summary

gold_branch_performance
