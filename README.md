# AI-Ops-Assistant-Order-Intelligence-System

This repository contains a working AI Ops automation workflow that processes incoming orders, evaluates operational constraints, and produces actionable decisions.
The system is built using n8n (no-code automation) and demonstrates real-world operational decision-making.

# Problem Statement

Operations teams must process orders while considering inventory availability, production capacity, and order priority.
Manual handling leads to delays, errors, and missed escalations.
This system automates decision-making for order processing using deterministic logic.

# Input Data

The workflow consumes two CSV files:

- orders.csv

OrderID, ProductCode, Quantity, OrderDate, Priority

- inventory.csv

ProductCode, AvailableStock

Files are read from Google Drive.

# Decision Logic (Core Workflow Behavior)

1. Orders and inventory are read and merged on ProductCode to enrich each order with available stock.

2. Each order is evaluated independently using conditional decision logic.

3. If inventory is missing or zero, the order is immediately escalated.

4. If order quantity exceeds available stock, the order is escalated for stock shortage.

5. If stock is sufficient, the order is checked against a fixed daily capacity threshold (200 units).

6. Orders within capacity are approved automatically.

7. Orders exceeding capacity are routed based on priority: urgent orders are split, normal orders are delayed.

8. Each order exits the workflow with exactly one decision, reason, and action.

9. All decision outputs are aggregated into a single result set before notification.

10. The workflow is deterministic and executes the same logic for every run.

# Failure Handling

- Missing or invalid inventory data routes orders to escalation paths.

- Type conversion is enforced to prevent numeric comparison errors.

- Each execution is deterministic and idempotent.

# Assumptions

- Input CSV files are well-formed and available at execution time.

- Product codes are consistent across datasets.

- Production capacity threshold is fixed at 200 units per run.

- Priority values are predefined (Urgent, Normal).

# Video

https://drive.google.com/file/d/1BIp5NgCIQ7nGNQsDKnnhFvICU0Pew95p/view?usp=drive_link
