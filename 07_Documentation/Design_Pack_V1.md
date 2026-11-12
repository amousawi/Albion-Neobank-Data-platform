# Albion NeoBank Design Pack V1

## Purpose

This document outlines the proposed design for the Albion NeoBank data platform before implementation begins.

The platform will ingest banking and payment provider datasets into Databricks and process the data through Bronze, Silver and Gold layers to support reporting and analytics.

## Scope

### Core Banking Sources
- customers.csv
- accounts.csv
- branches.csv
- transactions.csv

### CRA Sources
- cra_2026-09_part1.csv
- cra_2026-09_part2.csv

### Payment Provider Sources
- Checkout.com
- Worldpay
- Adyen
- Stripe

## File Formats

- CSV
- JSONL

## Target Platform

- Databricks Free Edition
- GitHub
- PySpark

## Design Status

Version: V1

Status: Draft

Implementation Approved: No

## Proposed Architecture

### Source Layer

The source layer consists of CSV and JSONL files received from multiple source systems.

Sources include:

- Customers
- Accounts
- Branches
- Transactions
- CRA
- Checkout.com
- Worldpay
- Adyen
- Stripe

### Storage Layer

All source files will be stored within a Databricks Managed Volume:

albion.default.albion_source_files

### Bronze Layer

Purpose:

- Store raw source data
- Preserve source records
- Capture ingestion metadata

Tables:

- bronze_customers
- bronze_accounts
- bronze_branches
- bronze_transactions
- bronze_cra
- bronze_checkoutcom
- bronze_worldpay
- bronze_adyen
- bronze_stripe

### Silver Layer

Purpose:

- Cleanse data
- Apply validation rules
- Remove duplicates
- Standardise formats

Tables:

- silver_customers
- silver_accounts
- silver_branches
- silver_transactions
- silver_payments

### Gold Layer

Purpose:

- Reporting
- KPI calculation
- Dashboard datasets
- Business analytics

Tables:

- gold_customer_summary
- gold_account_summary
- gold_transaction_summary
- gold_branch_performance


## Entity Relationship Model

The platform will use the following relationships:

Branches (1) → (Many) Customers

Branches (1) → (Many) Accounts

Customers (1) → (Many) Accounts

Accounts (1) → (Many) Transactions

### Primary Keys

Branches:
- branch_code

Customers:
- customer_id

Accounts:
- account_id

Transactions:
- txn_id

### Foreign Keys

Customers:
- branch_code

Accounts:
- customer_id
- branch_code

Transactions:
- account_id
