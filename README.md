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

Orders and inventory are read and merged on ProductCode to enrich each order with available stock.

Each order is evaluated independently using conditional decision logic.

If inventory is missing or zero, the order is immediately escalated.

If order quantity exceeds available stock, the order is escalated for stock shortage.

If stock is sufficient, the order is checked against a fixed daily capacity threshold (200 units).

Orders within capacity are approved automatically.

Orders exceeding capacity are routed based on priority: urgent orders are split, normal orders are delayed.

Each order exits the workflow with exactly one decision, reason, and action.

All decision outputs are aggregated into a single result set before notification.

The workflow is deterministic and executes the same logic for every run.
