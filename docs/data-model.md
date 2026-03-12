# Simplified Data Model

## Core entities

The data model is built around a simplified set of operational entities:

- Project
- Work Item
- Status
- User / Responsible Person
- Event
- Baseline Snapshot

## Storage layers

### 1. Raw ingestion layer
Purpose:
- keep incoming source data in a minimally transformed form
- support troubleshooting
- preserve source traceability

Examples:
- raw events
- raw snapshots
- source payload references

### 2. Current state layer
Purpose:
- store the latest known state of core entities
- support operational lookups and reporting joins

Examples:
- current projects
- current work items
- current assignments
- current statuses

### 3. Event log layer
Purpose:
- capture meaningful changes over time
- support historical analysis and auditability

Examples:
- status changes
- reassignment events
- date changes
- planning or baseline changes

### 4. Reporting layer
Purpose:
- provide BI-ready and query-friendly structures
- simplify dashboard logic
- expose operational metrics

Examples:
- overdue work summary
- project status overview
- current vs. baseline comparison
- change trend summaries

## Design principles

### Relational modeling
The model uses stable keys and clear relationships between core entities to support consistent joins and reporting.

### Idempotent processing
The ingestion logic is designed to avoid duplicate records during repeated sync runs or repeated event delivery.

### Historical visibility
Changes are stored in a way that allows analysis of both current state and evolution over time.

### Reporting-first design
Reporting structures are intentionally separated from raw ingestion data to make downstream analytics easier and more reliable.

## Simplified logical structure

### Projects
Represents the top-level operational context.

### Work Items
Represents tasks, activities, or process units linked to a project.

### Events
Represents meaningful actions or changes affecting projects or work items.

### Baseline Snapshots
Represents point-in-time planning or reference data used for comparison against current execution.

### Reporting Views
Represents aggregated or transformed structures optimized for dashboards and summaries.
