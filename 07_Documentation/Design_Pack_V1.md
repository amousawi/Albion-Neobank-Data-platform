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
