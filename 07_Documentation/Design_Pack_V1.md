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

## Data Flow Design

The platform will process data through the following stages:

Source Files
│
├── CSV Files
│     ├── Customers
│     ├── Accounts
│     ├── Branches
│     ├── Transactions
│     ├── CRA
│     ├── Checkout.com
│     └── Worldpay
│
├── JSONL Files
│     ├── Adyen
│     └── Stripe
│
▼

Managed Volume
(albion.default.albion_source_files)

▼

Bronze Layer

Store source data in its original structure with audit metadata.

▼

Silver Layer

Apply:
- Data type conversion
- Duplicate removal
- Business validation
- Standardisation

▼

Gold Layer

Produce:
- Reporting datasets
- KPI datasets
- Dashboard datasets
- Business analytics outputs

▼

## Medallion Layer Design

### Bronze Layer

Purpose:
Store raw source data with minimal transformation.

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

Additional metadata columns:

- ingestion_timestamp
- source_file_name
- batch_id

---

### Silver Layer

Purpose:
Store cleansed and validated data.

Tables:

- silver_customers
- silver_accounts
- silver_branches
- silver_transactions
- silver_payments

Transformations:

- Data type conversion
- Duplicate removal
- Null validation
- Data standardisation
- Business rule validation

---

### Gold Layer

Purpose:
Provide business-ready datasets.

Tables:

- gold_customer_summary
- gold_account_summary
- gold_transaction_summary
- gold_branch_performance

Business Outputs:

- Customer metrics
- Account metrics
- Transaction KPIs
- Branch performance reporting

Dashboard and Reporting Layer

## Metadata Framework Design

### Purpose

The metadata framework will allow source systems and files to be onboarded without requiring significant code changes.

### Metadata Captured

For each source dataset the platform will store:

- Source system name
- Source file name
- File format
- Target Bronze table
- Load type
- Primary key
- Ingestion timestamp
- Batch identifier
- Processing status

### Benefits

- Configuration-driven ingestion
- Simplified onboarding of new datasets
- Improved auditability
- Reduced maintenance effort
- Consistent processing across sources

### Example Metadata Record

| Source System | File Format | Bronze Table | Primary Key |
|---------------|-------------|--------------|------------|
| Customers | CSV | bronze_customers | customer_id |
| Accounts | CSV | bronze_accounts | account_id |
| Transactions | CSV | bronze_transactions | txn_id |
| Adyen | JSONL | bronze_adyen | payment_id |

## Audit and Logging Design

### Purpose

The audit framework will provide visibility of all data processing activities and support operational monitoring.

### Audit Information Captured

The platform will record:

- Source system
- Source file name
- Batch identifier
- Load start time
- Load end time
- Record count
- Success status
- Failure status
- Error message

### Audit Process

During each ingestion process:

1. Load starts
2. Start timestamp captured
3. File processed
4. Record counts calculated
5. Success or failure status recorded
6. End timestamp captured

### Benefits

- Traceability
- Operational monitoring
- Failure investigation
- Data quality reporting
- Historical load tracking

### Example Audit Record

| Batch ID | Source | Records | Status |
|-----------|----------|----------|----------|
| B001 | customers.csv | 3000 | SUCCESS |
| B002 | accounts.csv | 4667 | SUCCESS |
| B003 | transactions.csv | 60000 | SUCCESS |
