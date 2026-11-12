# Architecture Decision Records

## ADR-001

### Decision
Databricks Free Edition will be used as the development platform.

### Reason
The project requirements can be implemented using Databricks Free Edition without requiring additional cloud infrastructure.

### Status
Approved

---

## ADR-002

### Decision
A Medallion Architecture (Bronze, Silver and Gold) will be used.

### Reason
This architecture provides clear separation between raw, validated and business-ready data.

### Status
Approved

---

## ADR-003

### Decision
Source files will be stored in a Databricks Managed Volume before ingestion.

### Reason
Managed Volumes provide a secure and organised location for storing source files before processing.

### Status
Approved

---

## ADR-004

### Decision
PySpark will be used as the primary processing language.

### Reason
PySpark is natively supported within Databricks and is suitable for scalable data engineering workloads.

### Status
Approved
