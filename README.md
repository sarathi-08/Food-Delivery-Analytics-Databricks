# 🍔 Food Delivery Analytics Pipeline

An end-to-end data engineering pipeline built on **Apache Spark** and **Databricks** that processes food delivery and sales data — covering batch analytics, Delta Lake operations, and real-time streaming ingestion.

---

## 📌 Project Overview

This project simulates a real-world food delivery analytics system. It covers the full data pipeline lifecycle:

- Ingesting raw CSV data into distributed storage
- Performing revenue and customer analytics using Spark SQL and DataFrame API
- Managing transactional data with Delta Lake (ACID operations)
- Building a real-time streaming pipeline using Auto Loader for incremental data ingestion

---

## 📂 Dataset Schema

### `food_delivery.csv`
| Column | Description |
|---|---|
| DeliveryID | Unique delivery identifier |
| OrderID (FK) | Foreign key linking to food_sales |
| CustomerName | Name of the customer |
| DeliveryDate | Date of delivery |
| DriverID | Assigned driver |
| RestaurantID | Restaurant identifier |
| DeliveryStatus | Status (Completed / Cancelled / Pending) |
| PaymentMethod | Mode of payment |
| DeliveryAddress | Delivery location |
| CustomerPhone | Contact number |

### `food_sales.csv`
| Column | Description |
|---|---|
| OrderID (PK) | Primary key |
| MenuItem | Name of food item ordered |
| Quantity | Number of units ordered |
| PricePerItem | Unit price |
| TotalPrice | Gross total |
| Discount | Discount applied |
| Tax | Tax amount |
| OrderDate | Date of order |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Distributed Processing | Apache Spark (PySpark) |
| Storage Format | Delta Lake |
| Streaming Ingestion | Auto Loader (cloudFiles) |
| Query Engine | Spark SQL |
| Notebook Environment | Databricks |
| Data Format | CSV |

---

## 🔧 Pipeline Architecture
Raw CSV Data

│

▼

DBFS / Volumes (Storage Layer)

│

├──► Spark DataFrame API → Revenue & Customer Analytics

│

├──► Spark SQL → JOIN queries, monthly trends, tax analysis

│

├──► Delta Tables → ACID operations (UPDATE, MERGE/Upsert)

│

└──► Auto Loader (Streaming) → Incremental ingestion with checkpointing

---

## 📊 Key Analytics Performed

### Section 1 — Batch Analytics
- **Monthly Revenue Analysis** — Grouped by `OrderDate` month to compute total revenue per month
- **Top 5 Menu Items** — Ranked by net revenue (`TotalPrice - Discount`)
- **Top 10 Customers by Spend** — JOIN across `food_sales` and `food_delivery` tables
- **Monthly Tax Revenue** — Aggregated tax collection trends over time

### Section 2 — Delta Lake Operations
- Created managed Delta tables from raw CSV for both datasets
- Performed targeted **UPDATE** — marking specific orders as `Completed`
- Executed **MERGE (Upsert)** — bulk status update for all `Cancelled` orders to `Not Delivered` using `DeltaTable.merge()`

### Section 3 — Auto Loader Streaming
- Configured Auto Loader with `cloudFiles` source format for schema inference and incremental ingestion
- Set up checkpoint and schema location for fault-tolerant streaming
- Demonstrated **exactly-once ingestion** — uploading `food_sales1.csv` then `food_sales2.csv` and verifying no duplicate processing via checkpointing
- Queried monthly revenue from streaming data using `try_cast` for type-safe aggregation

---

## 🗂️ Repository Structure
Food-Delivery-Analytics-Databricks/

│

├── Sarathi_HON_nb.html        # Exported notebook with all outputs

├── Sarathi_HON_nb.dbc         # Databricks archive (importable)

├── food_delivery.csv          # Primary delivery dataset

├── food_sales.csv             # Sales transactions dataset

└── README.md

---

## 🚀 How to Run

### Option 1 — Import DBC into Databricks
1. Log in to your Databricks workspace
2. Go to **Workspace → Import**
3. Upload `Sarathi_HON_nb.dbc`
4. Upload the CSV files to DBFS or Volumes
5. Update file paths in the notebook and run all cells

### Option 2 — View Notebook Output
Open `Sarathi_HON_nb.html` directly in any browser to view the full notebook with all outputs — no Databricks account required.

---

## 💡 Key Technical Highlights

- Handled **RDD restrictions on shared clusters** by switching to the DataFrame API — producing equivalent results with better performance
- Resolved **Auto Loader schema inference** issues by explicitly configuring `cloudFiles.schemaLocation`
- Fixed **CAST_INVALID_INPUT errors** on string-typed numeric columns using `try_cast()` instead of direct `CAST`

---

## 📈 Skills Demonstrated

`PySpark` `Spark SQL` `Delta Lake` `Auto Loader` `Structured Streaming` `DataFrame API` `ACID Transactions` `Data Ingestion` `Databricks`

---

## 👤 Author

**Sarathi V**
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://rb.gy/llmcjd)
[![GitHub](https://img.shields.io/badge/GitHub-sarathi--08-black)](https://github.com/sarathi-08)
